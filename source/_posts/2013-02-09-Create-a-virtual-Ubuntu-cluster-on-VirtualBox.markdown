---
layout: post
title: "Create a virtual Ubuntu cluster on VirtualBox"
date: 2013-02-09 09:27:42 UTC
updated: 2013-02-09 09:27:42 UTC
comments: true
categories: Cluster Linux
---

1. Create a virtual machine
1. Change the network to bridge mode
1. Install Ubuntu Server OS
1. Setup the hostname to something like "node-01"
1. Boot up the new virtual machine
1. Remove some network rules
`sudo rm -rf /etc/udev/rules.d/70-persistent-net.rules`
1. Clone the virtual machine
1. Initialize with a new MAC address
1. Boot up the cloned virtual machine
1. Edit /etc/hostname: change "node-01" to "node-02"
1. Edit /etc/hosts: change "node-01" to "node-02"
1. Reboot the cloned virtual machine
1. Repeat step 7 to 13 until there are enough nodes

Note: the ip address of each node should start with "192.168." unless you don't have a router.

