---
layout: post
title: Creating Command-line application in python
comments: true /*disqus comments enabled for this post*/
description: Learning how to build a good command-line application in Python
keywords: python, argparse, click, command-line, terminal, usage, pyinstaller 
---

Many a times Dev-Ops folks love to have a command-line application rather than going to the browser and doing things. And yes, why not. Command-line applications are a lot faster than the browser and can be scripted eaisly.
In this post I am wrting about how to build a command-line application in Python.

When I say command-line application one thing that urgently strikes to my mind is I have to build something like "ping" having various options like '-a','-v' and also having a pretty 'usage'.
Hence inorder to build such type of application you have to think about parsing arguments from command-line.

There are various tools our there which makes it easy to build a command-line application. Some of the examples are:
1. Click
2. Clint
3. docopt
4. Cliff

I started off by using Click. Click provide you with good api's in order to create nested commands for your application. It also has its own way to handle user credentials and printing the usage string. Its pretty neat if you are looking to build a commmand line appliction which will be dependent upon python. But in my case I had to build an application which shall be independent of the fact that whether the user has python installed on his/her machine or no. In order to achieve this the best option left with me was to use something which comes with python installation itself. Hence I decided to move with argparse. arparse is not liked much by the python community because it is more code to write when compared to the above modules like Click or Clint. But it also has good documentation in place and once you get familiar with its functionality you start liking it. 

My aim was to build a command line application with nested command which will do different things for the user. To give you an example it should look something like this:
<p class="message"> 
$myCommandLineApplication doSomething -withThis String -alsoWithThis String
</p>

Now, if you observe, we cant just use Parser.ArgumentParser() and parse the strings given as command line arguments. We need something like subparser in order to tell the command line application that doSomething is supposed to parse the strings and not myCommandLineApplication. And just as we want argparse has a function called subparser which can be used in order to achieve the above goal.

