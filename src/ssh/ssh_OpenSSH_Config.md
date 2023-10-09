[Voltar](OpenSSH_Guide.md)

#  Configuring an OpenSSH Server

Parent page: [Internet and Networking](https://help.ubuntu.com/community/InternetAndNetworking) >> [SSH](https://help.ubuntu.com/community/SSH)

Conteúdo
- [Configuring an OpenSSH Server](#configuring-an-openssh-server)
  - [Introduction](#introduction)
  - [Disable Password Authentication](#disable-password-authentication)
  - [Disable Forwarding](#disable-forwarding)
  - [Specify Which Accounts Can Use SSH](#specify-which-accounts-can-use-ssh)
  - [Rate-limit the connections](#rate-limit-the-connections)
  - [Log More Information](#log-more-information)
  - [Troubleshooting](#troubleshooting)


[Voltar](OpenSSH_Guide.md)

## Introduction

Once you have installed an OpenSSH server,

```
sudo apt-get install openssh-server 
```

you will need to configure it by editing the sshd\_config file in the /etc/ssh directory.

<table><tbody><tr><td><p><img alt="IconsPage/tip.png" src="https://help.ubuntu.com/community/IconsPage?action=AttachFile&amp;do=get&amp;target=tip.png" title="IconsPage/tip.png"></p></td><td><p><tt>sshd_config</tt> is the configuration file for the OpenSSH <em>server</em>. <tt>ssh_config</tt> is the configuration file for the OpenSSH <em>client</em>. Make sure not to get them mixed up.</p></td></tr></tbody></table>

First, make a backup of your sshd\_config file by copying it to your home directory, or by making a read-only copy in /etc/ssh by doing:

```
sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.factory-defaults
sudo chmod a-w /etc/ssh/sshd_config.factory-defaults
```

Creating a read-only backup in /etc/ssh means you'll always be able to find a known-good configuration when you need it.

Once you've backed up your sshd\_config file, you can make changes with any text editor, for example;

```
sudo gedit /etc/ssh/sshd_config
```

runs the standard text editor in Ubuntu 12.04 or more recent. For older versions replace "sudo" with "gksudo". Once you've made your changes (see the suggestions in the rest of this page), you can apply them by saving the file then doing:

```
sudo restart ssh
```

If you get the error, "Unable to connect to Upstart", restart ssh with the following:

```
sudo systemctl restart ssh
```

Configuring OpenSSH means striking a balance between security and ease-of-use. Ubuntu's default configuration tries to be as secure as possible without making it impossible to use in common use cases. This page discusses some changes you can make, and how they affect the balance between security and ease-of-use. When reading each section, you should decide what balance is right for your specific situation.

## Disable Password Authentication

Because a lot of people with SSH servers use weak passwords, many online attackers will look for an SSH server, then start guessing passwords at random. An attacker can try thousands of passwords in an hour, and guess even the strongest password given enough time. The recommended solution is to use [SSH keys](https://help.ubuntu.com/community/SSH/OpenSSH/Keys) instead of passwords. To be as hard to guess as a normal SSH key, a password would have to contain 634 random letters and numbers. If you'll always be able to log in to your computer with an SSH key, you should disable password authentication altogether.

If you disable password authentication, it will only be possible to connect from computers you have specifically approved. This massively improves your security, but makes it impossible for you to connect to your own computer from a friend's PC without pre-approving the PC, or from your own laptop when you accidentally delete your key.

_It's recommended to disable password authentication unless you have a specific reason not to._

To disable password authentication, look for the following line in your sshd\_config file:

**#PasswordAuthentication yes**

replace it with a line that looks like this:

**PasswordAuthentication no**

Once you have saved the file and [restarted your SSH server](http://www.cyberciti.biz/faq/howto-start-stop-ssh-server/), you shouldn't even be asked for a password when you log in.

## Disable Forwarding

By default, you can tunnel network connections through an SSH session. For example, you could connect over the Internet to your PC, tunnel a [remote desktop](https://help.ubuntu.com/community/VNC) connection, and access your desktop. This is known as "port forwarding".

By default, you can also tunnel specific graphical applications through an SSH session. For example, you could connect over the Internet to your PC and run nautilus "file://$HOME" to see your PC's home folder. This is known as "X11 forwarding".

While both of these are very useful, they also give more options to an attacker who has already guessed your password. Disabling these options gives you a little security, but not as much as you'd think. With access to a normal shell, a resourceful attacker can replicate both of these techniques and a specially-modified SSH client.

_It's only recommended to disable forwarding if you also use [SSH keys with specified commands](https://help.ubuntu.com/community/SSH/OpenSSH/Keys#keys-with-specific-commands)_.

To disable forwarding, look for the following lines in your sshd\_config:

and replace them with:

If either of the above lines don't exist, just add the replacement to the bottom of the file. You can disable each of these independently if you prefer.

## Specify Which Accounts Can Use SSH

You can explicitly allow or deny access for certain users or groups. For example, if you have a family PC where most people have weak passwords, you might want to allow SSH access just for yourself.

Allowing or denying SSH access for specific users can significantly improve your security if users with poor security practices don't need SSH access.

_It's recommended to specify which accounts can use SSH if only a few users want (not) to use SSH._

To allow only the users Fred and Wilma to connect to your computer, add the following line to the bottom of the sshd\_config file:

To allow everyone except the users Dino and Pebbles to connect to your computer, add the following line to the bottom of the sshd\_config file:

It's possible to create very complex rules about who can use SSH - you can allow or deny specific groups of users, or users whose names match a specific pattern, or who are logging in from a specific location. For more details about how to create complex rules, see the [sshd\_config man page](http://manpages.ubuntu.com/manpages/hardy/man5/sshd_config.5.html)

## Rate-limit the connections

It's possible to limit the rate at which one IP address can establish new SSH connections by [configuring the uncomplicated firewall](https://help.ubuntu.com/community/UFW) (ufw). If an IP address is tries to connect more than 10 times in 30 seconds, all the following attempts will fail since the connections will be DROPped. The rule is added to the firewall by running a single command:

```
sudo ufw limit ssh
```

On a single-user or low-powered system, such as a laptop, the number of total simultaneous pending (not yet authorized) login connections to the system can also be limited. This example will allow two pending connections. Between the third and tenth connection the system will start randomly dropping connections from 30% up to 100% at the tenth simultaneous connection. This should be set in sshd\_config.

In a multi-user or server environment, these numbers should be set significantly higher depending on resources and demand to alleviate denial-of-access attacks. Setting a lower the login grace time (time to keep pending connections alive while waiting for authorization) can be a good idea as it frees up pending connections quicker but at the expense of convenience.

## Log More Information

By default, the OpenSSH server logs to the AUTH facility of syslog, at the INFO level. If you want to record more information - such as failed login attempts - you should increase the logging level to VERBOSE.

_It's recommended to log more information if you're curious about malicious SSH traffic._

To increase the level, find the following line in your sshd\_config:

and change it to this:

Now all the details of ssh login attempts will be saved in your /var/log/auth.log file.

If you have started using a different port, or if you think your server is well-enough hidden not to need much security, you should increase your logging level and examine your auth.log file every so often. If you find a significant number of spurious login attempts, then your computer is under attack and you need more security.

Whatever security precautions you've taken, you might want to set the logging level to VERBOSE for a week, and see how much spurious traffic you get. It can be a sobering experience to see just how much your computer gets attacked.

If you want to try to scare novice attackers, it can be funny to display a banner containing legalese. This doesn't add any security, because anyone that's managed to break in won't care about a "no trespassing" sign--but it might give a bad guy a chuckle.

To add a banner that will be displayed before authentication, find this line:

and replace it with:

This will display the contents of the /etc/issue.net file, which you should edit to your taste. If you want to display the same banner to SSH users as to users logging in on a local console, replace the line with:

To edit the banner itself try

```
sudo gedit /etc/issue.net
```

Here is an example for what you might put in an issue or issue.net file and you could just copy&paste this in:

```
***************************************************************************
                            NOTICE TO USERS


This computer system is the private property of its owner, whether
individual, corporate or government.  It is for authorized use only.
Users (authorized or unauthorized) have no explicit or implicit
expectation of privacy.

Any or all uses of this system and all files on this system may be
intercepted, monitored, recorded, copied, audited, inspected, and
disclosed to your employer, to authorized site, government, and law
enforcement personnel, as well as authorized officials of government
agencies, both domestic and foreign.

By using this system, the user consents to such interception, monitoring,
recording, copying, auditing, inspection, and disclosure at the
discretion of such personnel or officials.  Unauthorized or improper use
of this system may result in civil and criminal penalties and
administrative or disciplinary action, as appropriate. By continuing to
use this system you indicate your awareness of and consent to these terms
and conditions of use. LOG OFF IMMEDIATELY if you do not agree to the
conditions stated in this warning.

****************************************************************************
```

## Troubleshooting

Once you have finished editing sshd\_config, make sure to save your changes before restarting your SSH daemon.

First, check that your SSH daemon is running:

```
ps -A | grep sshd
```

This command should produce a line like this:

```
<some number> ?        00:00:00 sshd
```

If there is no line, your SSH daemon is not running. If it is, you should next check that it's listening for incoming connections:

```
sudo ss -lnp | grep sshd
```

This command should produce a line that looks like one of these:

```
0  128  :::22  :::*  users:(("sshd",16893,4))
0  128   *:22   *:*  users:(("sshd",16893,3))
```

If there is more than one line, in particular with a port number different than 22, then your SSH daemon is listening on more than one port - you might want to go back and delete some Port lines in your sshd\_config. If there are no lines, your SSH daemon is not listening on any ports, so you need to add at least one Port line. If the line specifies something other than "\*:22" (\[::\]:22 is IPv6), then your SSH daemon is listening on a non-standard port or address, which you might want to fix.

Next, try logging in from your own computer:

```
ssh -v localhost
```

This will print a lot of debugging information, and will try to connect to your SSH server. You should be prompted to type your password, and you should get another command-line when you type your password in. If this works, then your SSH server is listening on the standard SSH port. If you have set your computer to listen on a non-standard port, then you will need to go back and comment out (or delete) a line in your configuration that reads Port 22. Otherwise, your SSH server has been configured correctly.

To leave the SSH command-line, type:

```
exit
```

If you have a local network (such as a home or office network), next try logging in from one of the other computers on your network. If nothing happens, you might need to tell your computer's firewall to allow connections on port 22 (or from the non-standard port you chose earlier).

Finally, try logging in from another computer elsewhere on the Internet - perhaps from work (if your computer is at home) or from home (if your computer is at your work). If you can't access your computer this way, you might need to tell your router's firewall to allow connections from port 22, and might also need to configure [Network Address Translation](https://help.ubuntu.com/community/ServersBehindNAT).

SSH/OpenSSH/Configuring (editada pela última vez em 2015-08-24 19:51:36 por ip174-70-35-183)