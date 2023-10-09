[Voltar](OpenSSH_Guide.md)

# Wikibook on OpenSSH

## Contents

- [Wikibook on OpenSSH](#wikibook-on-openssh)
  - [Contents](#contents)
    - [Introduction\[edit | edit source\]](#introductionedit--edit-source)
    - [Client-Server\[edit | edit source\]](#client-serveredit--edit-source)
    - [Utilities\[edit | edit source\]](#utilitiesedit--edit-source)
    - [Logging, Troubleshooting, and Development\[edit | edit source\]](#logging-troubleshooting-and-developmentedit--edit-source)
    - [Cookbook\[edit | edit source\]](#cookbookedit--edit-source)
  - [References\[edit | edit source\]](#referencesedit--edit-source)

  
The OpenSSH suite provides secure remote access and file transfer.<sup id="cite_ref-OpenSSH_homepage_1-0"><a href="https://en.wikibooks.org/wiki/OpenSSH#cite_note-OpenSSH_homepage-1">[1]</a></sup> Since its initial release, it has grown to become the most widely used implementation of the SSH protocol. During the first ten years of its existence, it had largely replaced older corresponding unencrypted tools and protocols. The OpenSSH client is included by default in most operating system distributions, including MacOS, AIX, Linux, BSD, and Solaris. Any day you use the Internet, you are using and relying on hundreds if not thousands of machines operated and maintained using OpenSSH. A survey in 2008 showed that of the SSH servers found running, just over 80% were OpenSSH. <sup id="cite_ref-OpenSSH_marketshare_2008_2-0"><a href="https://en.wikibooks.org/wiki/OpenSSH#cite_note-OpenSSH_marketshare_2008-2">[2]</a></sup> Even with the advent of the Internet of Things and the increased use of IPv6, a cursory search of Shodan <sup id="cite_ref-OpenSSH_marketshare_shodan_3-0"><a href="https://en.wikibooks.org/wiki/OpenSSH#cite_note-OpenSSH_marketshare_shodan-3">[3]</a></sup> for SSH-2.0 services on port 22 in November 2022 showed 87% of responding addresses running OpenSSH. <sup id="cite_ref-4"><a href="https://en.wikibooks.org/wiki/OpenSSH#cite_note-4">[4]</a></sup>

OpenSSH was first released towards the end of 1999. It is the latest step in a very long and useful history of networked computing, remote access, and telecommuting.

This book is for fellow users of OpenSSH to help save effort and time through using OpenSSH, and especially SFTP, where it makes sense to use it.

### Introduction\[[edit](https://en.wikibooks.org/w/index.php?title=OpenSSH&veaction=edit&section=1 "Edit section: Introduction") | [edit source](https://en.wikibooks.org/w/index.php?title=OpenSSH&action=edit&section=1 "Edit section's source code: Introduction")\]

-   [Overview](https://en.wikibooks.org/wiki/OpenSSH/Overview "OpenSSH/Overview")
-   [Why Use Encryption](https://en.wikibooks.org/wiki/OpenSSH/Why_Use_Encryption "OpenSSH/Why Use Encryption")
-   [SSH Protocols](https://en.wikibooks.org/wiki/OpenSSH/SSH_Protocols "OpenSSH/SSH Protocols")
-   [Other SSH Implementations](https://en.wikibooks.org/wiki/OpenSSH/Other_SSH_Implementations "OpenSSH/Other SSH Implementations")

### Client-Server\[[edit](https://en.wikibooks.org/w/index.php?title=OpenSSH&veaction=edit&section=2 "Edit section: Client-Server") | [edit source](https://en.wikibooks.org/w/index.php?title=OpenSSH&action=edit&section=2 "Edit section's source code: Client-Server")\]

-   [Client Applications](https://en.wikibooks.org/wiki/OpenSSH/Client_Applications "OpenSSH/Client Applications")
-   [Client Configuration Files](https://en.wikibooks.org/wiki/OpenSSH/Client_Configuration_Files "OpenSSH/Client Configuration Files")
-   [OpenSSH Server](https://en.wikibooks.org/wiki/OpenSSH/Server "OpenSSH/Server")
-   [Pattern Matching in OpenSSH Configuration](https://en.wikibooks.org/wiki/OpenSSH/Pattern_Matching_in_OpenSSH_Configuration "OpenSSH/Pattern Matching in OpenSSH Configuration")

### Utilities\[[edit](https://en.wikibooks.org/w/index.php?title=OpenSSH&veaction=edit&section=3 "Edit section: Utilities") | [edit source](https://en.wikibooks.org/w/index.php?title=OpenSSH&action=edit&section=3 "Edit section's source code: Utilities")\]

-   [Utilities](https://en.wikibooks.org/wiki/OpenSSH/Utilities "OpenSSH/Utilities")
-   [Third Party Utilities](https://en.wikibooks.org/wiki/OpenSSH/Third_Party_Utilities "OpenSSH/Third Party Utilities")

### Logging, Troubleshooting, and Development\[[edit](https://en.wikibooks.org/w/index.php?title=OpenSSH&veaction=edit&section=4 "Edit section: Logging, Troubleshooting, and Development") | [edit source](https://en.wikibooks.org/w/index.php?title=OpenSSH&action=edit&section=4 "Edit section's source code: Logging, Troubleshooting, and Development")\]

-   [Logging and Troubleshooting](https://en.wikibooks.org/wiki/OpenSSH/Logging_and_Troubleshooting "OpenSSH/Logging and Troubleshooting")
-   [Development](https://en.wikibooks.org/wiki/OpenSSH/Development "OpenSSH/Development")

### Cookbook\[[edit](https://en.wikibooks.org/w/index.php?title=OpenSSH&veaction=edit&section=5 "Edit section: Cookbook") | [edit source](https://en.wikibooks.org/w/index.php?title=OpenSSH&action=edit&section=5 "Edit section's source code: Cookbook")\]

-   [Remote Processes](https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Remote_Processes "OpenSSH/Cookbook/Remote Processes")
-   [Tunnels](https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Tunnels "OpenSSH/Cookbook/Tunnels")
-   [Automated Backup](https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Automated_Backup "OpenSSH/Cookbook/Automated Backup")
-   [File Transfer with SFTP](https://en.wikibooks.org/wiki/OpenSSH/Cookbook/File_Transfer_with_SFTP "OpenSSH/Cookbook/File Transfer with SFTP")
-   [Public Key Authentication](https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Public_Key_Authentication "OpenSSH/Cookbook/Public Key Authentication")
-   [Certificate-based Authentication](https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Certificate-based_Authentication "OpenSSH/Cookbook/Certificate-based Authentication")
-   [Host-based Authentication](https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Host-based_Authentication "OpenSSH/Cookbook/Host-based Authentication")
-   [Load Balancing](https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Load_balancing "OpenSSH/Cookbook/Load balancing")
-   [Multiplexing](https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Multiplexing "OpenSSH/Cookbook/Multiplexing")
-   [Proxies and Jump Hosts](https://en.wikibooks.org/wiki/OpenSSH/Cookbook/Proxies_and_Jump_Hosts "OpenSSH/Cookbook/Proxies and Jump Hosts")

## References\[[edit](https://en.wikibooks.org/w/index.php?title=OpenSSH&veaction=edit&section=6 "Edit section: References") | [edit source](https://en.wikibooks.org/w/index.php?title=OpenSSH&action=edit&section=6 "Edit section's source code: References")\]

1.  [↑](https://en.wikibooks.org/wiki/OpenSSH#cite_ref-OpenSSH_homepage_1-0 "Jump up") ["OpenSSH"](http://www.openssh.com/). www.openssh.com.
2.  [↑](https://en.wikibooks.org/wiki/OpenSSH#cite_ref-OpenSSH_marketshare_2008_2-0 "Jump up") ["Statistics from the current scan results"](http://www.openssh.com/usage/ssh-stats.html). OpenSSH.com. 2008.
3.  [↑](https://en.wikibooks.org/wiki/OpenSSH#cite_ref-OpenSSH_marketshare_shodan_3-0 "Jump up") ["SSH-2.0 Search Results"](https://www.shodan.io/search?query=ssh-2.0). shodan.io. Retrieved 2022-11-07.
4.  [↑](https://en.wikibooks.org/wiki/OpenSSH#cite_ref-4 "Jump up") At that time, 87% was 17,093,847 out of 19,715,171 systems. Dropbear made up about 6% at 1,092,738 systems and then a long tail filled in the rest. A Shodan search including non-standard ports, not just port 22, showed noticeably more SSH services (25,520,277) whereof 83% (21,215,882) where OpenSSH.