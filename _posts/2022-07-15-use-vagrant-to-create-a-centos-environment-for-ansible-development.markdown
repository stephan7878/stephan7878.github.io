---
layout: post
title:  "Use Vagrant to create a CentOS environment for Ansible development"
author: "Stephan Bester"
date:   2022-07-15 04:12:00 +0200
categories: [ansible, centos, vagrant]
---

![vagrant]({{ "/assets/2022-07-15-vagrant.png" | relative_url }}){: width="30%" style="float: left; margin-right: 1em;" }
I recently wanted to test Ansible playbooks locally, but since I am on a Windows environment, this proved a little difficult. It is possible to install Ansible in WSL, but I found that this did not quite fit my need, since I wanted a control node where I can tweak and run the Ansible scripts from, but also needed some target machines to apply the changes to. This gave me the idea to use another tool I am very fond of, Vagrant, to create several Linux machines to create my Ansible development environment.

This is an excerpt from a blog posted on the IBM Community site. Read the full post [here](https://community.ibm.com/community/user/cloud/blogs/stephan-bester/2022/07/05/use-vagrant-to-create-a-centos-environment-for-ans){:target="\_blank" :rel="noopener noreferrer"}.
