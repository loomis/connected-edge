---
layout: default-edit
title: Custom Applications
nav_order: 8
parent: Edge Computing (11/2019)
description: Custom Applications
permalink: /docs/edge-computing/custom-apps
---

# Custom Applications

 * Run either the tensorflow image classification or object detection
   example on the RPi. This requires access to a raspberry pi camera.

 * Modify the tensorflow image classification or object detection
   example to work with images taken from a standard webcam. This will
   require changing the use to use OpenCV for the image samples rather
   than the picamera python module.

 * Define a custom application that will analyze some data on the edge
   device and send events (alerts, notifications, etc.) to an
   application running in the cloud. The cloud application should
   visualize the events. Verify that the entire processing chain works
   correctly.
