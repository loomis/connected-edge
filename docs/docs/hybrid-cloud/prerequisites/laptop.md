---
layout: default-edit
title: Local Machine
nav_order: 1
parent: Prerequisites
grand_parent: Hybrid Cloud (07/2019)
permalink: /docs/hybrid-cloud/prerequisites/laptop
---

# Local Machine

To interact with the cloud services and edge devices, you must have a
local machine (laptop or workstation) that is connected to the
Internet and that provides a Linux (or Linux-like) environment with a
modern web browser.

The following sections provide alternatives, listed from most
desirable to least desirable.

## Native Linux OS

The best configuration is the use of a laptop or workstation that
natively runs a Linux or Linux-like operating system. There are many
alternatives, most of which can be installed easily on recent
hardware.

If you are installing Linux on your machine, you may want to consider
some of these alternatives:

 - [Ubuntu Desktop](https://ubuntu.com/download/desktop): A common,
   well maintained distribution that aims to keep software versions
   close to the latest releases. You should prefer a distribution with
   long term support (LTS). Ubuntu 18.04 is currently the lastest LTS
   release.

 - [Linux Mint](https://www.linuxmint.com/): A distribution based on
   Ubuntu and Debian that provides an excellent graphical user
   interface with full multimedia support.

 - [CentOS](https://www.centos.org/): Derived from the RedHat
   Enterprise Linux (RHEL) distribution, it provides a very stable
   Linux environment with descent desktop support. (Be sure to include
   desktop utilities when installing.)

 - [OpenBSD](https://www.openbsd.org/): An operating system that
   prioritizes security. It uses its own, non-Linux kernel, but
   provides the standard command line utilities needed for this
   training.

You can also search the web for other alternatives. There are a large
number that make different tradeoffs between usability, latest
software releases, and security.

## MacOS

MacOS available on Apple's laptops and workstations provides an
excellent Linux-like environment. This is a standard part of the
distribution and can be used without having to install any additional
software. The downside is that the Apple hardware is relatively more
expensive than hardware with similar specifications from other
vendors. 

## Ubuntu on Windows 10

If you have a Windows 10 machine and do not want to change the
operating system, [Ubuntu on
Windows](https://www.microsoft.com/en-us/p/ubuntu/9nblggh4msv6)
provides the Ubuntu Linux interface as an application running within
Windows 10. Ubuntu provides [detailed
information](https://tutorials.ubuntu.com/tutorial/tutorial-ubuntu-on-windows)
for installing and starting Ubuntu on Windows 10.

Once installed, this provides a terminal with a complete set of the
standard Linux command line tools. It is also possible to install
additional Linux software as needed. 

## Linux Virtual Machine

It is possible to install a virtualization platform (hypervisor) on
your Windows machine and then create a virtual machine using one of
the Linux distributions. There are essentially two options:
Microsoft's
[Hyper-V](https://docs.microsoft.com/en-us/virtualization/hyper-v-on-windows/about/)
and [VirtualBox](https://www.virtualbox.org/).

The hypervisor takes a significant amount of CPU and memory
resources. Unless you have a very capable laptop, the interactive
response for this solution is likely to be very frustrating.

## PuTTY on Windows

PuTTY is a Secure Shell (SSH) client for Windows. This provides the
minimum interface necessary to log into remote cloud and edge
resources with the SSH protocol. Information about installing,
configuring, and using PuTTY can be found on its
[website](https://www.chiark.greenend.org.uk/~sgtatham/putty/).

This configuration should be used only as a last resort. It is awkward
to use and provides only a subset of the tools available in the more
complete alternatives listed above.


