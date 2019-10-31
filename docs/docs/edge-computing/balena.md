---
layout: default-edit
title: BalenaCloud
nav_order: 6
parent: Edge Computing (11/2019)
description: BalenaCloud
permalink: /docs/edge-computing/balena
---

# BalenaCloud

 * Create an account linked to your GitHub identity
 
 * Create an application: simply a name for a group of machines
   running the same program/analysis.

   - The name is arbitrary. Choose something simple but unique.

 * Create a device: one (physical) machine that provides computing
   resources for running the given program/analysis.

   - Choose to run a 64-bit development operating system.
   - You can then download the customized image.
   - Copy this to your SD card.
   - Boot the machine and wait for the machine to become visible in
     the Balena console.

 * Create a release: The program/analysis to be run on the
   machines. These are packaged as a container.

   - Follow the instructions for running their example "release".
   - Once this works, deploy one of your example applications and
     verify that it works on the device.
   - Do the same for the OpenCV example. How are peripherials
     allocated to a given "release"?

 * Understand the deployment and management model of BalenaCloud. What
   does BalenaCloud add compared to just a collection of RPi machines?
   What is the primary entity (program, device, etc.)? How are the
   entities in the platform related?
