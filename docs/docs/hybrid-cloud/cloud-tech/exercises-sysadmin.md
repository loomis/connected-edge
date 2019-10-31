---
layout: default-edit
title: Exercises-System-Admin
nav_order: 8
parent: Cloud Technologies
grand_parent: Hybrid Cloud (07/2019)
permalink: /docs/hybrid-cloud/cloud-tech/exercises-sysadmin
---

# System Administration

Before diving into creating cloud applications, it is necessary that
you understand a bit about system administration, specifically package
and service management. The instructions are given below for Ubuntu
18.04 and CentOS 7. Choose the operating system with which you're most
comfortable, although it is useful to look through the information for
both systems.

## Ubuntu 18.04

### Super User

System administration commands must be run from the "root"
(super user) account.

Normally with Ubuntu, you will log into the "ubuntu" account, which is
a normal user account, not a super user account. To run system
administration commands from the "ubuntu" account, there are two
options:

 - Prefix each command with `sudo`. This command will switch
   temporarily to the super user account and execute the command given
   to `sudo`.

 - Switch into the "root" account with the command "sudo su -". This
   creates a new session with the "root" account. System administrator
   accounts can be run with a `sudo` prefix. To close the "root" shell
   and return to the "ubuntu" account, just type `exit`. 

On Exoscale, there is also a third option. The Exoscale Ubuntu images
are configured so that you can SSH directly into the root account.
Just change the command: `ssh ubuntu@ipv4-address` to `ssh
root@ipv4-address`. 

### Package Management

| description | command |
| --- | --- |
| update cache | `apt update` |
| list all available packages | `apt list` |
| list installed packages | `apt list --installed` |
| search for package | `apt search STRING` |
| install package | `apt install PACKAGE` |
| remove package | `apt remove PACKAGE` |

Try all of these command to understand how they work. Try searching,
installing, and removing the "nginx" package. Nginx is one of the
standard web servers.

### Editors

To administer services on a virtual machine, you will need to be able
to edit configuration files. The editors that are installed by default
on Ubuntu 18.04 are: `nano` and `vi`. You need to be familiar with one
of them. If you're not already familiar with `vi`, choose `nano`.  It
has a very short learning curve.  You can also install `emacs`
(package name "emacs-nox") if you're familiar with it.

### Service Management

Services are normally managed with the `systemctl` command (and
friends). The full service management subsystem is called
[systemd](https://www.freedesktop.org/wiki/Software/systemd/). Earlier
Ubuntu operating systems used a different system management system.

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

To understand how these commands work, reinstall the "nginx"
package. When the service is started, you should be able to see the
default landing page with the command:

```
curl http://localhost
```

This will dump the raw HTML content.  In the HTML, you should see a
header element like `<h1>Welcome to nginx!</h1>`. 

Try to do the same from outside of the machine. It will likely fail
because the server cannot be contacted from your browser. There are
probably two reasons why.  Can you think of what they could be?

The first reason is probably that your default security group on
Exoscale is not configured correctly.  We opened ports for `ping` and
`ssh`, not for HTTP(S). Can you modify your default security group to
open the ports 80 (HTTP) and 443 (HTTPS)?

The second reason is probably a local firewall running on your VM. The
local firewall filters network traffic **in addition to** the security
group. Rather than configuring both the security group and local
firewall, it is generally easier just to disable the local
firewall. The name of the local firewall service on Ubuntu is
"ufw". Can you use the system administrator commands to disable it?

### IP Address

You will often need to find the IP address of your virtual
machine. You can always get this from Exoscale, but it often easier to
get this from within the VM itself.  There are many ways to do this,
but the easiest is just `ifconfig`.  Look for the "inet" value
assigned to the "eth0" interface.

## CentOS 7 

### Super User

System administration commands must be run from the "root"
(super user) account.

Normally with CentOS on Exoscale, you will log into the "centos"
account, which is a normal user account, not a super user account. To
run system administration commands from the "centos" account, there
are two options:

 - Prefix each command with `sudo`. This command will switch
   temporarily to the super user account and execute the command given
   to `sudo`.

 - Switch into the "root" account with the command "sudo su -". This
   creates a new session with the "root" account. System administrator
   accounts can be run with a `sudo` prefix. To close the "root" shell
   and return to the "centos" account, just type `exit`.

On Exoscale, there is also a third option. The Exoscale CentOS images
are configured so that you can SSH directly into the root account.
Just change the command: `ssh centos@ipv4-address` to `ssh
root@ipv4-address`.

### Package Management

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

### Editors

To administer services on a virtual machine, you will need to be able
to edit configuration files. The `vi` editor is installed by default
on CentOS 7.

If you're not already familiar with `vi`, you may want to install
`nano`.  It has a very short learning curve.  Just run `yum install
nano`. You can also install `emacs` (package name "emacs-nox") if
you're familiar with it.

### Service Management

Services are normally managed with the `systemctl` command (and
friends). The full service management subsystem is called
[systemd](https://www.freedesktop.org/wiki/Software/systemd/). Earlier
CentOS operating systems used a different system management system.

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

To understand how these commands work, reinstall the "nginx"
package. When the service is started, you should be able to see the
default landing page with the command:

```
curl http://localhost
```

This will dump the raw HTML content.  In the HTML, you should see a
title element like `<title>Test Page for the Nginx HTTP Server on
Fedora</title>`.

Try to do the same from outside of the machine. It will likely fail
because the server cannot be contacted from your browser. There are
probably two reasons why.  Can you think of what they could be?

The first reason is probably that your default security group on
Exoscale is not configured correctly.  We opened ports for `ping` and
`ssh`, not for HTTP(S). Can you modify your default security group to
open the ports 80 (HTTP) and 443 (HTTPS)?

The second reason is probably a local firewall running on your VM. The
local firewall filters network traffic **in addition to** the security
group. Rather than configuring both the security group and local
firewall, it is generally easier just to disable the local
firewall. The name of the local firewall service on CentOS is
"firewalld". Can you use the system administrator commands to disable
it?

### IP Address

You will often need to find the IP address of your virtual
machine. You can always get this from Exoscale, but it often easier to
get this from within the VM itself.  There are many ways to do this,
but the easiest is just `ifconfig`.  Look for the "inet" value
assigned to the "eth0" interface.

