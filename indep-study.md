---
# Copyright (C) 2016 Anthony DeDominic
#
# Permission is granted to copy, distribute and/or modify this document
# under the terms of the GNU Free Documentation License, Version 1.3
# or any later version published by the Free Software Foundation;
# with no Invariant Sections, no Front-Cover Texts, and no Back-Cover Texts.
# A copy of the license is included in the section entitled "GNU
# Free Documentation License".

# The build requires the following dependencies:
#    TeXLive
#    pandoc 
#    pandoc-citeproc
---

1. Introduction
===============

Given the fast paced world of information technology, there aren't many cross platform tools to automate deployment, manage and maintenance of infrastructure.

Most operating systems offer basic UIs through remote shells.
The problem with this is that remote shells usually lack the power to affect complex change.
They are also potentially limited by lack of tools available.

Many of the coreutils in shells are built around processing and modifying line oriented data--tools like: sed, grep, paste, cut, tr, xargs, etc.
However such tools make it difficult to work with more modern configuration files and service oriented architecture.
Because of this, many common automation tools leverage powerful scripting languages, like python.
This is because unlike most shells, scripting languages usually have facilities and datastructures for handling tree objects and various other common data structures.

tools have been made that leverage standard libraries in scripting languages: Puppet, Chef, Ansible, Salt Stack and many others.
These tools exist to turn lisp-like abstract syntax trees and compose collections of functions, or modules, into executable jobs.

1.1. Related Works
------------------

### 1.1.1. Ansible

Ansible is one of the popular tools in the space.
It leverages Python--and Powershell for Windows, to create a full automation framework.

Because of ansible's popularity, but also its shortcomings, many projects were built around ansible.
Examples are projects like loopabull which add web technology to ansible to make it responsive to events.
Even more complex projects like Ansible Tower add UIs and charts to ansible to make it more user friendly.

### 1.1.2. Puppet

Puppet is a tool that is very similar to Ansible, however puppet is dependent on a backend service--like Foreman, to function properly.
For the most part, Ansible is slowly supplanting Puppet from the space.

2. Background
=============

2.1. Continuous Integration and Continuous Deployment
-----------------------------------------------------

CICD is the process of accelerating the building, testing and installation of applications to end servers .
In a world where web technology moves fast and new features are ideal, it's critical to go to market fast.
To do this there are two major architectures that are used.

CI, continuous integration is concerned with the development process.
In the realm of continuous integration there is usually a source code repository.
The source code repository is usually technologies like git, svn, cvs or other version and source controlling software.
The idea of the source code repository is to allow for efficient ways to handle code changes and to manage multiple developers working on the same code.

Lastly, there is a server, running software similar to Jenkins CI or Travis CI which can potentially handle many tasks.
At a high level, it is usually used to run a build or test step in, say, a build.gradle, project.json, Makefile or various other build tools.
To enhance tools like Jenkins, there are binary and other code quality scans like SonarQube and others which attempt to find issues outside of the space of unit and mock tests.
Other such triggers, like diff checking, can be used to trigger code reviews for massive revisions of source code.

Generally, the final stage of Continuous Integration is to notify the developers, or other interested parties, the results of these various tests and builds.
In a full CICD build pipeline, generally there is the process of uploading so called artifacts to a artifact or binary repository.
These binary repositories are more in the realm of continuous delivery.

Continuous delivery also has it's share of tools and structure.
One of the first requirements of continuous delivery is having some form of binary repository.
For java based projects, there are things like nexus.
Other languages, like python, have their own packaging sites;
python for instance has PyPI.

In order to deploy these binaries, many tools make use of remote shell protocols.
Remote shell protocols give tools access to execute the needed steps to get software deployed.
Generally these tools run through scripts which make the machine require the needed binaries and create the needed configurations.
The remote shells are no different than conventional user-controlled shells.

There are various tools and servers that do this; a few examples are Ansible, uDeploy and Puppet.
Ansible uses remote shell protocols, such as secure shell (ssh), to execute a set of instructions written in yaml, generally with the intent of installing some type of software.
uDeploy is similar in how it causes change on target machines, using secure shell; however uDeploy generally requires the target machines to be running some kind of daemon.

Many POSIX-like systems make use of package management to deliver software.
Packages, like .deb's and .rpm's, are a collection of installation shell scripts, including pre-installation and post-installation, and a binary or source code.
Package managers, as their name implies, also manages these installed binaries, scripts and configurations.
Part of their management requires tracking file locations. This allows for rolling back, upgrading or removal of installed files.

Deployment strategy can be different depending on the available infrastructure.
In an environment with fixed inventory, it might not be ideal to do things like \`make install\` which are hard to reverse.
However in an environment where machines can be spun up at whim, or even automatically, it wouldn't matter as much; in such cases one would simply destroy and create a new machine for every deployment.
In a fixed architecture, it might be ideal to stick to package management solutions for delivering binaries.
It might not matter if it is dynamic as the cleanliness of the system.

2.2. JavaScript, NodeJS and other Technologies
-----------------------------------------------


