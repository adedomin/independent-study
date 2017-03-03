---
# Copyright (C) 2017 Anthony DeDominic
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

title: "devops-foundry: Multi-purpose DevOps tool"
abstract: |
  *Dev Ops, CICD and Agile workplaces require fast delivery to market.*
  *To achieve this, developers and system administrators need advanced, cross-platform automation tools.*
  *This paper is concerned with a new automation tool that attempts to address limitations of Ansible.*
  *This is accomplished having a module system that is easy to develop for and allows for finer control over the flow of execution.*
  *Automation frameworks could greatly benefit by implementing these features.*
  *This is demonstrated by comparing DevOps-FoundryJS to Ansible.*
papersize: letter
geometry: margin=2cm
fontfamily: mathpazo
fontsize: 12pt
header-includes:
- \hyphenpenalty 10000
- \usepackage{fancyhdr}
- \pagestyle{fancy}
- \fancyfoot[L]{DeDominic - AutomateJS}
- \fancyfoot[C]{Independent Study - \the\year}
- \fancyfoot[R]{\thepage}
- \author{DeDominic, Anthony\\Eastern Connecticut State University\\Willimantic, USA\\dedominica@my.easternct.edu}

link-citations: Yes
references:


- title: 'jcom: A JavaScript Object Shell'
  URL: 'https://github.com/adedomin/CSC450-project-written/blob/master/final/CSC450-SEN-dedominica.pdf'
  author:
  - family: DeDominic
    given: Anthony
  id: jcom
  type: article-journal
  issued:
    year: 2016

- title: Ansible Documentation
  URL: 'http://docs.ansible.com/ansible'
  publisher: Ansible
  id: ansible

- title: Introduction to browserify
  URL: 'https://writingjavascript.org/posts/introduction-to-browserify#_=_'
  author:
  - family: Vincent
    given: Seth
  id: browserify
  issued:
    year: 2017

- title: Puppet Documentation
  URL: 'https://docs.puppet.com/puppet/'
  publisher: Puppet
  id: puppet

- title: 'Lessons from using Ansible exclusively for 2 years.'
  URL: 'https://blog.serverdensity.com/what-ive-learnt-from-using-ansible-exclusively-for-2-years/'
  author:
  - family: Raun
    given: Corban
  id: lessons-ansible
  issued:
    year: 2015

- title: 'Jenkins CI documentation'
  URL: 'https://jenkins.io/doc/'
  publisher: Jenkins
  id: jenkins

- title: 'Jenkins Plugins'
  URL: 'https://plugins.jenkins.io/'
  publisher: Jenkins
  id: jenkins-plugins
---
