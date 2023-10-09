[Voltar](OpenSSH_Guide.md)

# Advanced OpenSSH Functions

Conteúdo
- [Advanced OpenSSH Functions](#advanced-openssh-functions)
  - [Introduction](#introduction)
  - [Tunneling VNC connections through ssh](#tunneling-vnc-connections-through-ssh)
  - [Mounting a remote directory](#mounting-a-remote-directory)
  - [Running from (x)inetd](#running-from-xinetd)
  - [Logging in with Kerberos](#logging-in-with-kerberos)
  - [Limiting the number of connections](#limiting-the-number-of-connections)
  - [Resources](#resources)
  - [Local System Resources](#local-system-resources)
  - [Ubuntu Wiki Resources](#ubuntu-wiki-resources)
  - [WWW Resources](#www-resources)


## Introduction

This page discusses a collection of advanced uses for SSH. This list is far from complete - it should only serve to get you thinking about possible uses.

## Tunneling VNC connections through ssh

Virtual Network Computing ("VNC") is a cross-platform way of sharing a desktop. Once you've set your SSH server up, see [VNC](https://help.ubuntu.com/community/VNC) for more information.

## Mounting a remote directory

The SSH protocol includes [SFTP](http://en.wikipedia.org/wiki/SSH_file_transfer_protocol) (the Secure File Transfer Protocol). Ubuntu can use SFTP to treat your SSH server rather like a removable drive. For example, if your Ubuntu computer has an SSH account on a computer called alpha-centauri, you could create a folder alpha-centauri in your home folder, then do the following:

```
sshfs -o idmap=user alpha-centuari: ~/alpha-centauri/
```

Now when you look in your alpha-centuari folder, you will see your home folder on alpha-centauri. You can safely remove this device by doing:

```
fusermount -u ~/alpha-centauri/
```

Although this SSH filesystem is extremely useful, it's not what the SFTP protocol was designed for. As such, some ordinary operations might not behave the way you'd expect - for example, you can't unmount an SSHFS directory from the file browser.

## Running from (x)inetd

The OpenSSH server can also be called into service as needed by the Internet Daemon, inetd, or its modern replacement, [xinetd](http://en.wikipedia.org/wiki/Xinetd). xinetd can be used for additional logging such as successful or unsuccessful login, access restriction even including time of day, cpu priority, and number of connections. There are many more possibilities. See the manual pages for xinetd.conf(5) or inetd.conf(5) for a full overview of inetd configuration options.

To configure sshd to be launched from xinetd, you must configure xinetd to listen on TCP port 22, and to run /usr/sbin/sshd -i when a connection is established. This is done by adding a file, /etc/xinetd.d/ssh, with the following contents:

```
service ssh
{
        socket_type     = stream
        protocol        = tcp
        wait            = no
        user            = root
        server          = /usr/sbin/sshd
        server_args     = -i
        per_source      = UNLIMITED
        log_on_failure  = USERID HOST
        banner          = /etc/banner.inetd.connection.txt
        banner_success  = /etc/banner.inetd.welcome.txt 
        banner_fail     = /etc/banner.inetd.takeahike.txt

        # access_times    = 08:00-16:25
        # log_on_success  = PID HOST DURATION TRAFFIC EXIT
        # instances       = 10
        # nice            = 10
        # bind            = 192.168.100.100
        # only_from       = 192.168.100.0
        # no_access       = 192.168.154.0
        # no_access       += 192.168.133.0
}
```

Two main disadvantages with inetd are that there can be a slight increase in the delay during the start of the connection and that sshd must be configured to allow launching from xinetd.

inetd has far fewer options and needs a change in the file inetd.conf

```
ssh    stream  tcp     nowait  root /usr/sbin/sshd -i
ssh    stream  tcp6    nowait  root /usr/sbin/sshd -i
```

## Logging in with Kerberos

[Kerberos](https://help.ubuntu.com/community/Kerberos) is a security system used in some large organizations. It allows a user to have a single company-wide password, that they use to log in to all their services.

[http://www.visolve.com/security/ssh\_kerberos.php](http://www.visolve.com/security/ssh_kerberos.php) has a detailed guide for configuring OpenSSH to leverage Kerberos as an authentication mechanism.

## Limiting the number of connections

If you allow passwords on your SSH server, you can use Ubuntu's firewall ([iptables](https://help.ubuntu.com/community/IptablesHowTo)) to limit the rate at which passwords can be guessed. This forces an attacker to probe your computer slowly, so it might take weeks or months to guess your password. But it also allows an attacker to stop anybody from logging in, by flooding the server with bogus connection attempts.

You should only try this if you fully understand how iptables works. As root, you can do this:

```
iptables -N rate-limit
iptables -A rate-limit -p tcp -m conntrack --ctstate NEW -m limit --limit 3/min --limit-burst 3 -j RETURN
iptables -A rate-limit -j DROP
iptables -I INPUT 1 -p tcp --dport 22 -j rate-limit
```

This will limit you computer to 3 SSH connection attempts per minute. To make this change permanent, you will need to save these rules in whatever way you normally do.

Note that if you are using UFW to manage your firewall, the above may be accomplished by a command that can be as simple as (in the case of a default configuration with ssh on port 22) "ufw limit ssh". For details see the corresponding section on the [ufw manpage](http://manpages.ubuntu.com/manpages/lucid/en/man8/ufw.8.html).

(This section was based in part on [DD-WRT's guide](http://www.dd-wrt.com/wiki/index.php/Preventing_Brute_Force_Attacks))

## Resources

Additional resources pertaining to the advanced configuration of OpenSSH for enhanced security appear below.

## Local System Resources

<table><tbody><tr><td><p><tt>man&nbsp;sshd</tt></p></td><td><p>System manual page for the <tt>sshd</tt> server daemon</p></td></tr><tr><td><span id="line-103"></span><p><tt>man&nbsp;sshd_config</tt></p></td><td><p>System manual page for the <tt>/etc/ssh/sshd_config</tt> configuration file</p></td></tr><tr><td><span id="line-104"></span><p><tt>man&nbsp;ssh-copy-id</tt></p></td><td><p>System manual page for the <tt>ssh-copy-id</tt> application</p></td></tr><tr><td><span id="line-105"></span><p><tt>man&nbsp;ssh-keygen</tt></p></td><td><p>System manual page for the <tt>ssh-keygen</tt> application</p></td></tr><tr><td><span id="line-106"></span><p><tt>~/.ssh/authorized_keys</tt></p></td><td><p>List of "authorized" public keys (with limiting options)</p></td></tr><tr><td><span id="line-107"></span><p><tt>/etc/ssh/sshd_config</tt></p></td><td><p>The OpenSSH Secure Shell Daemon (<tt>sshd</tt>) configuration file</p></td></tr></tbody></table>

## Ubuntu Wiki Resources

-   [OpenSSH 4.3 VPNs](https://help.ubuntu.com/community/SSH_VPN) describes how to create a Virtual Private Network with recent versions of SSH.
    
-   [GPG & OpenSSH](https://help.ubuntu.com/community/GPGsigningforSSHHowTo) describes how to use GPG to sign SSH keys.
    

## WWW Resources

[Keeping SSH access secure](http://www.debian-administration.org/articles/87)

[OpenSSH Website](http://www.openssh.org/)

[Password-less logins with OpenSSH](http://www.debian-administration.org/articles/152)

[sshd under inetd / xinetd](http://en.wikibooks.org/wiki/OpenSSH/Server#sshd_under_inetd_.2F_xinetd)

SSH/OpenSSH/Advanced (editada pela última vez em 2012-10-11 08:52:28 por dsl-roibrasgw1-fe8ffb00-252)