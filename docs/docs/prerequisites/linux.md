---
layout: default-edit
title: Linux Operating System
nav_order: 2
parent: Prerequisites
permalink: /docs/prerequisites/linux
---

# Linux Operating System

Most virtual machines in the cloud and devices on the edge run Linux
operating systems. Moreover, these systems typically run in "headless"
mode, meaning that there is no attached monitor or graphical output by
default.

Because of this, you must have a good understanding of the Linux
operating system and how to use the operating system from the command
line. Some of the important aspects for this training are covered
below, but you should investigate the linked resources for a fuller
understanding of Linux.

## Shells

Use of Linux through the command line always takes place through a
"shell". This is a special program that allows interactive use of a
Linux system and that provides features that simplify interactions
with the operating system.

The Bourne shell (`sh`) is the original UNIX shell. All recent Linux
distributions support this shell and have it installed by
default. Most system level shell utilities target the command line
syntax of the Bourne shell to maximize portability between Linux
flavors. Details on this shell can be found on the web, for example,
in the [Bourne Shell
Scripting](https://en.wikibooks.org/wiki/Bourne_Shell_Scripting) book
on Wikibooks.

The most common shell for interactive use is the Bourne Again Shell
(`bash`). This version, provided by the GNU Project, provides some
additional features that make it easier to use than the plain Bourne
Shell, while still being fully compatible with the Bourne Shell
syntax. This is the default shell for most Linux distributions,
although it may not be present on embedded Linux distributions that
aim for a small footprint. Shell examples in this training use
`bash`. A [bash scripting
book](https://en.wikibooks.org/wiki/Bash_Shell_Scripting) is also
available in Wikibooks.

There are many other shells that can be used. The Z shell (`zsh`), C
shell (`csh`), `tcsh`, and Korn shell (`ksh`) are a few of them. These
may or may not be installed by default by a Linux distribution. In all
cases, use of these shells requires explicit configuration of your
user account. Documentation for these shells can be found on the
web. Unless you are already familiar with one of these shells, you
would be better served with `sh` or `bash`.

## Scripting

Automation of common actions or processes is often done by creating a
"shell script".  This is simply a text file that starts with a
"shebang" line followed by the shell commands to execute. An example
that prints "Hello World" to the terminal is:

```
#!/bin/bash

echo "Hello World"
```

The "shebang" line (first line starting with '#!') indicates what
shell or program to start to interpret the subsequent commands.

You should review the [Guide to
UNIX](https://en.wikibooks.org/wiki/Guide_to_Unix) and the
documentation for the shell that you use.

## System Administration

Before creating cloud applications, it is necessary that you
understand a bit about system administration, specifically package and
service management.

The instructions are given below for Ubuntu 18.04 and CentOS 7, two
common operating systems. Choose the operating system with which
you are most comfortable, although it is useful to look through the
information for both systems.

### Ubuntu 18.04

#### Administrator

System administration commands must be run from the "root" (super user
or administrator) account.

Normally with Ubuntu, you will log into the "ubuntu" account, which is
a normal user account, not an administrator account. To run system
administration commands from the "ubuntu" account, there are two
options:

 - Prefix each command with `sudo`. This command will switch
   temporarily to the super user account and execute the command given
   to `sudo`.

 - Switch into the "root" account with the command `sudo su -`. This
   creates a new session with the "root" account. System administrator
   accounts can be run with a `sudo` prefix. To close the "root" shell
   and return to the "ubuntu" account, just type `exit`. 

On many cloud providers, there is also a third option. Many Ubuntu
cloud images are configured so that you can SSH directly into the root
account.  Just change the command: `ssh ubuntu@ipv4-address` to `ssh
root@ipv4-address`.

#### Package Management

| description | command |
| --- | --- |
| update cache | `apt update` |
| list all available packages | `apt list` |
| list installed packages | `apt list --installed` |
| search for package | `apt search STRING` |
| install package | `apt install PACKAGE` |
| remove package | `apt remove PACKAGE` |

Understand how all these commands work. If you have access to an
Ubuntu machine, try searching, installing, and removing the "nginx"
package. Nginx is one of the standard web servers.

#### Editors

To administer services on a virtual machine, you will need to be able
to edit configuration files. The editors that are installed by default
on Ubuntu 18.04 are: `nano` and `vi`. You need to be familiar with one
of them. If you're not already familiar with `vi`, choose `nano`.  It
has a very short learning curve.  You can also install `emacs`
(package name "emacs-nox") if you're familiar with it.

#### Service Management

Services are normally managed with the `systemctl` command (and
friends). The full service management subsystem is called
[systemd](https://www.freedesktop.org/wiki/Software/systemd/). Earlier
Ubuntu operating systems used a different service management system.

| action | command |
| --- | --- |
| help | `systemctl --help` |
| service status | `systemctl status SERVICE` |
| status of all services | `systemctl status` | 
| service start | `systemctl start SERVICE` |
| service stop | `systemctl stop SERVICE` |
| service restart | `systemctl restart SERVICE` |
| enable service for start at boot | `systemctl enable SERVICE` |
| disable service | `systemctl disable SERVICE` |
| service output | `journalctl -u SERVICE` |

To understand how these commands work, reinstall the "nginx" package
on an Ubuntu machine. When the service is started, you should be able
to see the default landing page with the command:

```
curl http://localhost
```

This will dump the raw HTML content.  In the HTML, you should see a
header element like `<h1>Welcome to nginx!</h1>`.

Try the various service management commands to understand how they
affect the nginx service.

#### IP Address

You will often need to find the IP address of your virtual
machine. You can always get this from Exoscale, but it often easier to
get this from within the VM itself.  There are many ways to do this,
but the easiest is just `ifconfig`.  Look for the "inet" value
assigned to the "eth0" interface.

### CentOS 7 

#### Administrator

System administration commands must be run from the "root"
(super user or administrator) account.

Normally with CentOS on Exoscale, you will log into the "centos"
account, which is a normal user account, not a super user account. To
run system administration commands from the "centos" account, there
are two options:

 - Prefix each command with `sudo`. This command will switch
   temporarily to the super user account and execute the command given
   to `sudo`.

 - Switch into the "root" account with the command `sudo su -`. This
   creates a new session with the "root" account. System administrator
   accounts can be run with a `sudo` prefix. To close the "root" shell
   and return to the "centos" account, just type `exit`.

On many cloud providers, there is also a third option. Many CentOS
cloud images are configured so that you can SSH directly into the root
account.  Just change the command: `ssh ubuntu@ipv4-address` to `ssh
root@ipv4-address`.

#### Package Management

| description | command |
| --- | --- |
| empty package cache | `yum clean all` |
| list installed packages | `yum list installed` or `rpm -qa` |
| list available packages | `yum list available` |
| search for package | `yum search STRING` |
| install package | `yum install PACKAGE` |
| remove package | `yum uninstall PACKAGE` |

The CentOS `yum` configuration only includes packages that are
strictly part of the RedHat Enterprise Linux distribution.  Many
useful packages are in a separate package repository called
[EPEL](https://fedoraproject.org/wiki/EPEL).

To include the EPEL repository, install the package "epel-release":

```
yum install epel-release
```

Unless you want to run a very minimal system, you will almost
certainly want to systematically include the EPEL repository.

Try all of the package management commands to understand how they
work. Try searching, installing, and removing the "nginx"
package. Nginx is one of the standard web servers. The package for
this is in EPEL, not the core CentOS repositories.

#### Editors

To administer services on a virtual machine, you will need to be able
to edit configuration files. The `vi` editor is installed by default
on CentOS 7.

If you're not already familiar with `vi`, you may want to install
`nano`.  It has a very short learning curve.  Just run `yum install
nano`. You can also install `emacs` (package name "emacs-nox") if
you're familiar with it.

#### Service Management

Services are normally managed with the `systemctl` command (and
friends). The full service management subsystem is called
[systemd](https://www.freedesktop.org/wiki/Software/systemd/). Earlier
CentOS operating systems used a different service management system.

| action | command |
| --- | --- |
| help | `systemctl --help` |
| service status | `systemctl status SERVICE` |
| status of all services | `systemctl status` | 
| service start | `systemctl start SERVICE` |
| service stop | `systemctl stop SERVICE` |
| service restart | `systemctl restart SERVICE` |
| enable service for start at boot | `systemctl enable SERVICE` |
| disable service | `systemctl disable SERVICE` |
| service output | `journalctl -u SERVICE` |

To understand how these commands work, reinstall the "nginx" package
on an Ubuntu machine. When the service is started, you should be able
to see the default landing page with the command:

```
curl http://localhost
```

This will dump the raw HTML content.  In the HTML, you should see a
title element like `<title>Test Page for the Nginx HTTP Server on
Fedora</title>`.

Try the various service management commands to understand how they
affect the nginx service.

#### IP Address

You will often need to find the IP address of your virtual
machine. You can always get this from Exoscale, but it often easier to
get this from within the VM itself.  There are many ways to do this,
but the easiest is just `ifconfig`.  Look for the "inet" value
assigned to the "eth0" interface.
