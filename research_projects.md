---
layout: page
title: Research Work
---

<h2><b>Masters Thesis - Next Generation Black-Box Web Application Vulnerability Analysis Framework </b></h2>
<p>
This thesis, presents a new approach to vulnerability analysis. The vulnerability analysis module presented uses a novel approach of Inductive Reverse Engineering (IRE) to understand and model the web application. IRE first attempts to understand the behavior of the web application by giving certain number of input/output pairs to the web application. Then, the IRE module hypothesizes a set of programs (in a limited language specific to web applications, called AWL) that satisfy the input/output pairs. These hypotheses takes the form of a directed acyclic graph (DAG). AWL vulnerability analysis module can then attempt to detect vulnerabilities in this DAG. Further, it generates the payload based on the DAG, and therefore this payload will be a precise payload to trigger the potential vulnerability (based on our understanding of the program). It then tests this potential vulnerability using the generated payload on the actual web application, and creates a verification procedure to see if the potential vulnerability is actually vulnerable, based on the web application’s response.</p>

Toward Inductive Reverse Engineering of Web Applications.
[Kevin liao](kevinliao.me), <b>[Tejas Khairnar](tejas619.github.io)</b>, Dr. Adam Doupe(adamdoupe.com)



<h2><b>Threat Intelligence and Analytics</b></h2>
<p>In this research work we propose an Automated Threat Intelligence fuSion framework (ATIS) that is able to take all sorts threat sources into account and discover new intelligence by connecting the dots of apparently isolated cyber events. Our framework consists of various intelligence modules viz., IOC module, Malware Analysis module, Bitcoin module, Social dynamics module.<br>

[Toward Inductive Reverse Engineering of Web Applications](http://sefcom.asu.edu/publications/towards-automated-threat-intelligence-fusion-cic2016.pdf)
Ajay Modi, Zhibo Sun, Anupam Panwar, <b>Tejas Khairnar</b>, Ziming Zhao, [Dr. Adam Doupe](adamdoupe.com), [Gail-Joon Ahn](http://www.public.asu.edu/~gahn1/), Paul Black