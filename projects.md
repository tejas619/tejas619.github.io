---
layout: page
title: Projects
---


<h2><b>Virtual Machine Introspection based IDS</b></h2>
<p>Implemented virtual machine introspection in C language over QEMU hypervisor to introspect guest virtual machine running on Linux OS. Using this introspection technique our application was successfully able to detect hidden process deployed using a rootkit. Our application for
introspecting Windows guest OS was implemented on the logic of detection of Direct Kernel Object Manipulation (DKOM) based rootkit attacks. To successfully detect hidden process on Unix based OS, we implemented detection of syscall hooks. Our application is able to introspect Windows XP, Windows 7, Ubuntu 14.04 and Fedora OS for intrusions like rootkits or malwares.</p>



<h2><b>SQL Injection Firewall</b></h2>
<p>Developed SQLInjection Firewall for php based web applications. The logic behind this implementation was to proxy every sql query made to the database via a firewall so that malicious sql queries can be filtered
before they get executed in the database. Our solution is also able to through specific exceptions denoting the attempt of an attacker to inject into a SQL database using conditions like always
true. Prevented from 2nd Order SQL injections attacks as well. All the queries getting executed on SQL database are proxy through the firewall, hence we
were able to defend against 2nd Order SQL injection attacks as well.</p>