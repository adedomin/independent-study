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

Tools like Ansible have come a far way to bridge this problem.
However, the moderate complexity and requirements to create and utilize Ansible modules make it difficult to extend it beyond it's standard base.
This problem exists because managing foreign dependencies in Python require things like a virtualenv.
One must also include the Ansible library to process the arguments in the module.

Prior to tools like Ansible, users were leveraging shells to automate server tasks.
This is because most operating systems offer basic UIs through remote shells.
These UIs give a user the ability to affect change on a system.
However, shells have various portibility issues;
utilities that may be on one server, may not exist on another server.

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

### 1.1.3. Package Managers

GNU/Linux distributions leverage package management tools to simplify the process of installing applications.
Many of these tools work similar to the above.
They contain files that should be deployed and a runbook to execute what is being installed.

The problem however, is that these tools are designed for more generic software installations.
They usually deploy very basic configurations and setups that may require modification.
Not only that, but many of these tools require root privileges to function properly; this can greatly hinder users who do not have such privileges, but must deploy certain software.
Package manager packages are usually inflexible about where they install software, generally discouraging local dynamic linking or statically linked binaries.
Package management tools were made prior to more modern continuous integration tools; this usually makes these tools more complex to use.
Probably the largest issue though, is general portability.
Every GNU/Linux distribution, even if they use the same package manager tool, can have wildly different names for the same set of software;
one GNU/Linux distribution could provide postfix as postfix-smtp, another could provided is as postfix-server and another could simply provide it as postfix.


2. Background
=============

This section is concerned with providing more detail on the problem domain being solved with this tool.
It will also briefly describe the technologies which enable this tool to function and why they matter.

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

JavaScript is a unique language.
Not only is it finding uses as a general scripting language, thanks to run-times like NodeJS, it is also the only language for front-end web development.
Because web environments have different standard library features compared to NodeJS, web developers have created tools to bridge the gap between the various JavaScript environments.

NodeJS uses a more modern, though potentially wasteful in some ways, dependency management system.
Unlike other scripting languages like Perl and Python, NodeJS will allow a user to package their dependencies either locally to the program, or globally.
This means a user does not need to use *virtual envrionments* to prevent installing dependencies globally.
This system also allows for a user to have projects that use different library versions, without worrying about conflict.

Unlike the transition from Python 2.x to Python 3.x, JavaScript ECMA6 and ECMA5 are completely backwards compatible.
The advantage of this is that users of JavaScript do not need to worry about communities splitting by newer JavaScript releases.
Even methods which are considered bad practice, like *with()*--a function from very early versions of JavaScript, are still in the language.

An example is CommonJS;
CommonJS, or require.js, is a JavaScript tool that polyfills the require() function available on NodeJS and enabled browsers to have more modular code.

Browserify is a tool that takes it a step further.
It takes all of these module require() calls, finds NodeJS specific library functions and reserved words, and creates a bundled JavaScript file, with all the polyfills and libraries required, in one source file that can be included using one \<script src="index.bundle.js"\>\</script\> tag.
This completely revolutionized front-end web development as it allowed users to make modules that are truly platform independent.
Combine this with browserify's transformation streams and one can convert and bundle NodeJS source to target other JavaScript engines like GJS--GNOME bindings for JavaScript.
Lastly, users can use this to bundle NodeJS programs into one executable source file.


3. Objectives
=============

The primary goal is to build a new Continuous Deployment and Configuration Management tool which rivals tools like Ansible.
The idea is to leverage the strengths of JavaScript, NodeJS and utilities like browserify to accomplish this.
Once a tool is developed, the goal is to build example deployment and configuration management runbooks to determine its suitability.

4. Results
==========

This section will concern itself with features of the tool, AutomateJS, how it works and how it compares with Ansible.

4.1. jscomposer
---------------

The function jscomposer is what generates the code automatejs uses.
Code generation, in this way, better suits how automatejs works.
This is because the code is not executed by the tool, but by the target hosts.

The advantage jscomposer has over how ansible code generates is that it gives users control on the flow of execution.
Users can use the native jscomposer modules like parallel and serial to dictate strictly how to execute the code.
This is unlike ansible which requires users to use pre, post, tasks and handlers to give a similar benefit.

Below is an example of how one can use jscomposer to create a JavaScript file that will install ezios[^ezios-loc]--a web application available on npm.

[^ezios-loc]: More info at: <https://github.com/GeneralUnRest/ezios>

```yaml
# flow control
# install app example
tasks:
- name: 'install app'
  serial:
  - name: 'create user'
    shell: 'useradd -m ezios'
  - name: 'create db path'
    shell: > 
      mkdir -p /home/ezios/.local/var/db/ezios;
      chown -R ezios /home/ezios/.local;
  - name: 'install app/configs'
    parallel:
    - name: 'install application'
      shell: 'npm install -g ezios'
    - name: 'configure applcation'
      template:
        source: ezios.config.js
        destination: /home/ezios/.mon.js
        variables:
          db_path: '/home/ezios/.local/var/db/ezios'
          api_key: 'a secret key =]'
    - name: 'create service'
      systemd-helper/create:
        service_name: 'ezios'
        description: 'ezios: monitoring tool'
        user: 'ezios'
        exec: '/usr/bin/monjs start'
        service_extra:
        - 'WorkingDirectory=/home/ezios'
  - name: 'start ezios'
    shell: > 
      systemd reload-daemon;
      systemd enable ezios.service;
      systemd start ezios.service
```

Currently, there are limited modules in automatejs which is why the shell module[^on-shell-mod] is used so much.
However, this example demonstrates what can be accomplished with automatejs.
Unlike a pure shell script, for instance, there is no easy mechanism to fill out templates in shells.
This alone makes it superior.
It is also purely asynchronous, so while the configuration is being written, the npm module could be downloading and installing a server application, called ezios.

[^on-shell-mod]: Note that the shell module is highly unlikely to be portable between Windows and GNU/Linux systems, however portable replacements can be made by the community.

Systemd-helper is another module which creates service files.
It was designed to be used as a standalone command-driven module, but because of how simple automatejs's plugin system is, a simple callack function like systemd-helper/create.js can be leveraged directly.

As explained, serial and parallel modules that are built into jscomposer give a higher level control of the flow of execution. 
This allows for crucial tasks, like creating the user and the directory to be done before anything is installed.
Contrast this with the use of pre-tasks and post-tasks in other tools like automatejs.

4.2. automatejs
---------------

AutomateJS is the core user interface for the program.
It composes all the various tools and elements required to create and execute runbooks.
Currently, the tool can take a list of variables, inventory files and a runbook to generate a JavaScript file.
This JavaScript file can then be deployed using ssh to applicable hosts.

However, it lacks many features that Ansible has.
For instance, Ansible can leverage web services for dynamic inventory.
Ansible also has many more advanced features when it comes to protecting information that can be stored in variables and their playbooks.

4.3. Modules
------------

Modules are probably the biggest enhancement over other tools.
Virtually any asynchronous function works with AutomateJS.
Modules are merely functions which accept a JavaScript object of arguments and a callback which has an error parameter and a result value.

```javascript
// basic modules
module.exports = (args, cb) => {
    cb(null, args)
}
```

Above demonstrates a perfectly valid module.
This demonstrates the simplicity of the system.
Ansible requires a little bit more, which requires the program to be aware of an arguments file or must leverage the Ansible python library.

5. Discussion
=============

Discussion section.
