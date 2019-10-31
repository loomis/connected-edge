---
layout: default-edit
title: Containers
nav_order: 3
parent: Edge Computing (11/2019)
description: Containers
permalink: /docs/edge-computing/containers
---

# Containers

 * Create a GitHub repository to hold code for your container
 * Define what your container will do (specialized web server,
   Wordpress, etc.).
 * Base your container on Ubuntu 18.04 (mainly for consistency, but
   importantly also to have a base image for all architectures)
 * Build your custom container and verify that it works when you
   deploy it locally on your development machine
 * Create a repository for the image on Docker Hub
 * Push image to Docker Hub to ensure that authorization works
 * Push all the code to GitHub
 * Authorize TravisCI to access your GitHub account
 * Setup automatic builds via Travis CI (see example-opencv repository
   for the (.travis.\*) files to add to your repository.
 * Verify that the Travis CI build works correctly and that your image
   with various architectures are present
 * Verify that this also works on a virtual machine deployed at Exoscale.
