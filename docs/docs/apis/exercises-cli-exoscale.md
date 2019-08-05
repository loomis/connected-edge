---
layout: default-edit
title: Exercises-CLI-Exoscale
nav_order: 2
parent: IaaS Programming Interfaces
permalink: /docs/apis/exercises-cli-exoscale
---

# Exercises CLI Exoscale

Exoscale provides a comprehensive Command Line Interface (CLI) for
their services. CLIs are often useful for quick scripting tasks that
automate some actions on the cloud.

An [Exoscale blog
post](https://community.exoscale.com/documentation/tools/exoscale-command-line-interface/)
covers basic installation and use of the CLI. 

## Installation

The process for all platforms is similar. Essentially, the process
consists of:

 - Download the package for your machine from the [Exoscale CLI
   releases](https://github.com/exoscale/cli/releases) on GitHub.

 - Install or unpack the package and ensure that it is available in
   your shell's `PATH`.

These are binary packages that depend on the operating system.  Be
sure to use the correct package. If you're on macOS, Homebrew can be
used instead of directly downloading a release.

To verify that the command line has been properly installed, run the
command:

```
$ exo version

exo 1.4.1 ad5f7a1 (egoscale 0.18.1)
```

As above, it should respond with the version number of the installed
CLI. To get detailed help, use the command `exo help`.

## Configuration

The Exoscale CLI must be configured with your API key and
secret. These values can be recovered from the Exoscale portal.

Log into the Exoscale portal and then navigate to the
"ACCOUNT/PROFILE" page. Near the top of that page, there will be an
"API Keys" tab. When you select that tab it should look like the
following screenshot.

![Exoscale API Key/Secret](assets/exoscale-api-keys.png)

On the machine where you've installed the Exoscale CLI, execute the
command `exo config`. This will interactively update your
configuration. If the prompt to add a new profile doesn't appear, just
hit return.

```
$ exo config

Good day! exo is already configured:
✔ dev@sixsq.com [Default]
[+] Do you wish to add another account? [yN]: y
[+] API Key [none]: ...add value...
[+] Secret Key [none]: ...add value...
Checking the credentials of "..."... success!

[+] Name [you@example.com]: 
✔ ch-gva-2
You chose "ch-gva-2"
[+] Make [cal.loomis@gmail.com] your default profile? [yN]: y
[+] Do you wish to add another account? [yN]: N
```

You can get the details of your configuration with the command:

```
$ exo config show you@example.com
┼──────────────────────┼─────────────────────────────────┼
│       ACCOUNT        │                                 │
┼──────────────────────┼─────────────────────────────────┼
│ Name                 │ you@example.com                 │
│ API Key              │ EXO...                          │
│ API Secret           │ ×××××××××××××××××××××××××××     │
│ Default Zone         │ ch-gva-2                        │
│ Default Template     │ Linux Ubuntu 18.04 LTS 64-bit   │
│ Compute API Endpoint │ https://api.exoscale.ch/compute │
│ Storage API Endpoint │ https://sos-{zone}.exo.io       │
│ DNS API Endpoint     │ https://api.exoscale.ch/dns     │
┼──────────────────────┼─────────────────────────────────┼
```

If there are no errors and everything looks correct, you're ready to
try using the CLI to provision resources. 

## Compute Lifecycle

With the Exoscale CLI installed and configured, you are now ready to
repeat the deployment lifecycle for a virtual machine.

For help with the create options run type `exo vm create --help`. As
before, create a tiny 