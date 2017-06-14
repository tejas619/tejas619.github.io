---
layout: page
title: Research Work
---

<h4>Masters Thesis - Next Generation Black-Box Web Application Vulnerability Analysis Framework </h4>
<p>
This thesis, presents a new approach to vulnerability analysis. The vulnerability analysis module presented uses a novel approach of Inductive Reverse Engineering (IRE) to understand and model the web application. IRE first attempts to understand the behavior of the web application by giving certain number of input/output pairs to the web application. Then, the IRE module hypothesizes a set of programs (in a limited language specific to web applications, called AWL) that satisfy the input/output pairs. These hypotheses takes the form of a directed acyclic graph (DAG). AWL vulnerability analysis module can then attempt to detect vulnerabilities in this DAG. Further, it generates the payload based on the DAG, and therefore this payload will be a precise payload to trigger the potential vulnerability (based on our understanding of the program). It then tests this potential vulnerability using the generated payload on the actual web application, and creates a verification procedure to see if the potential vulnerability is actually vulnerable, based on the web application’s response.</p>

<h4>Virtual Machine Introspection based IDS</h4>
<p>Implemented virtual machine introspection in C language over QEMU hypervisor to introspect guest virtual machine running on Linux OS. Using this introspection technique our application was successfully able to detect hidden process deployed using a rootkit. Our application for
introspecting Windows guest OS was implemented on the logic of detection of Direct Kernel Object Manipulation (DKOM) based rootkit attacks. To successfully detect hidden process on Unix based OS, we implemented detection of syscall hooks. Our application is able to introspect Windows XP, Windows 7, Ubuntu 14.04 and Fedora OS for intrusions like rootkits or malwares.</p>

<h4>Threat Intelligence and Analytics (TIA)</h4>
<p>Graduate Research Assistant under Dr.Gail-joon Ahn of School of Computing, Informatics and Decision Systems at ASU. Worked as a Python developer for threat intelligence and analytics project. This tool gains its intelligence from four modules namely, Malware,
SocialSEAL, Bitcoin and IOC (Indicators of Compromise). As a system administrator for the Linux box running Cuckoo Sandbox, I was responsible to maintain the whole repository of analyed as well as new malware samples crawled from variosu public sources. Wrote scripts in order to populate data analyzed by cuckoo malware analysis tool into Neo4j Graph database. Developed RESTApi in python for the threat intelligence system.</p>