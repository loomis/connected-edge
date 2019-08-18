---
layout: default-edit
title: Secure Shell (SSH)
nav_order: 3
parent: Prerequisites
permalink: /docs/prerequisites/ssh
---

# Secure Shell (SSH)

You will use the Secure Shell (SSH) to interact with remote cloud and
edge resources. SSH is a system that uses a defined protocol, client,
and servers to govern access to remote resources. Users and machines
(hosts) are identified through cryptographic keys.

Digital Ocean has a good tutorial that covers the [SSH
Essentials](https://www.digitalocean.com/community/tutorials/ssh-essentials-working-with-ssh-servers-clients-and-keys).

The important commands for this training are:

| command | description |
| --- | --- |
| `ssh-keygen` | creates a new SSH key pair |
| `ssh` | opens a shell or executes a command on remote machine |
| `scp` | copies a file from/to a remote machine |

Be sure to understand the syntax of these commands and how they work.

## SSH Keys

It is extremely important to understand how SSH uses key pairs to
identify users (and hosts).  Each user is identified by a key pair,
which consists of a private key and a public key. As implied by the
names, the private key must be kept secret by the user, while the
public key can be shared with other people and machines.

In normal usage, a user has a single key pair, which is used to log
into multiple cloud or edge machines. A rough analogy is a passport. A
person normally has a single passport which allows that person access
to multiple countries. Unlike a passport, you only show the public key
to others; the private key remains a secret that is not shown to
anyone else.

On a Linux system, the normal location for the public and private keys
are:

```
~/.ssh/id_rsa.pub
~/.ssh/id_rsa
```

respectively. In many cases, a private key generated **without a
password** is easier to use. 

## Host Keys

Like people, machines are also identified via key pairs. When logging
into a remote machine the first time, you will either:

 - Be asked to trust a host key ("yes" will trust the host and add it
   to your "known hosts file) or 

 - See a warning that the host has been added automatically to your
   "known hosts" file. 

This list is stored by default in the file:

```
~/.ssh/known_hosts
```

This is a simple text file which you can view. Any host that you no
longer trust can be removed by just deleting the line for that host.
