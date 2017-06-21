---
layout: post
title: How to SSH into home computer from Work network
---

Every company has some kind of internet access policy in order to keep their network secure. According to this policy sometimes you cannot access social media websites like facebook, instagram etc. In this blog post I will guide you on how to ssh into your home computer and access blocked websites at your workplace leveraging the same. *** Violation of Company's security policy can cost you ***

## Installing ssh on your home machine

For Mac Users:<br>
Its pretty straight forward. Go to "System Preferences" > "Sharing" > "Remote login". Enable remote login for particular usrers on the Mac. Some of the configurations related to securing ssh are explained later in this post. 

For Linux Users:<br>
Follow the following commands in order to install OpenSSH-Server on your linux box.<br>
<p class="message"> 
sudo apt-get install openssh-server
</p>
Just follow the instructions and OpenSSH-server will be installed on your linux box. 

## Securing SSH service
Now, we also have to secure the ssh service we just started on our machine. All the configuration related to ssh service are in the file "sshd_config". Any changes made in this file are the changes made for the ssh service.
You should make the following changes to implement some level of secuirty for your ssh service. (These changes are mostly generic for ssh service keeping aside the platform) <br>
**Use public/private key pairs for authentication instead of passwords**
Generate a passphrase-protected SSH key for every computer that need access to the ssh home machine. In our case we will create this on our work machine.
<p class="message">
ssh-keygen -t rsa -b 2048 -v 
</p>
Here ssh-keygen unix based utility generates authentication keys for ssh. Using -t option you can specify the type of key to create. I am specifying RSA as cryptography type for my ssh-key because RSA algorithm is right now compatible with most of the ssh versions and -b option to specify the number of bits to be generated. 2048 bit RSA key is pretty strong against factoring of RSA modulus. I use -v to get pretty messages about the key generation. Btw, its verbose. <br>
<p class="message">
ssh-copy-id -i ~/.ssh/id_rsa.pub user@publicip
</p>
Here we copy the key we generated for the work machine into the home machine. The user will be the users who are allowed access to your home machine. The "publicip" thing I will exaplin further.<br> 

**Disable Password Access**<br>
Now that we have configured keys in order to ssh into home machine we can disable the password based access. This prevents us from the password bruteforce attacks.
The password access can be disabled by:<br>
<p class="message">
#PasswordAuthentication yes<br>
PasswordAuthentication no
</p>
**Disable RootLogin**<br>
We should not allow root users to login via ssh. This can be done by: <br>
<p class="message">
#PermitRootLogin no <br>
PermitRootLogin no
</p>
**Limit the number of users that can ssh into your home machine** <br>
We can achieve this by adding a line into sshd_config file about allowing specific users or specific group of users to login via ssh.
This can be done by adding this line at the end of sshd_config: <br>
<p class="message">
AllowUsers user1 user2
</p>
**Using ssh protocol 2** <br>
SSh protocol 1 has number of security vulnerabilities of which exploits are available publicly. Hence we should only use ssh protocol 2 for our purpose.
This can be done by uncommenting the protocol line in sshd_config and mentioning the number '2'.

## Knowning your public IP address 
Now that we have our SSH service running on our home machine we can move ahead on how to access your home machine from work place. The first and foremost requirement in order to achieve this is to know the Public IP of your home network. I am assuming that you have a router placed at your home to which all your devices are connected. There are many ways in order to find the Public IP of your router. The following are two of my ways:

*  Login into your router. <br>
	This is the most geneuine way inorder to know the details of the internet connection you are using at your home. For me the IP details were in the "Internet Port" tab of the management console.<br> 

*  [https://www.whatismyip.com/]<br>

## Configuring your router
We know the Public IP of our router now. Lets go ahead with some network related stuff to make this work. 
Public IP's are accessible from everywhere in the world. That's why they are called Public. :)
But your home machine is NATted behind your router. By this I mean that your router performs some kind of address translation from PrivateIP > PublicIP and vice versa whenever you access internet at home. You can verfiy this by checking your IP address configuration. It would be most probably start with "192.168". Now, the question is, how will our router recognize that I want to access which device on myhome network? <br>
There are many ways to achieve this, but the first thought ways are as:

**Port Forwarding**<br>
"A port forward is a way of making a computer on your home or business network accessible to computers on the internet, even though they are behind a router. (https://portforward.com/)"
In order to make this work we have to login into the management console of the home router and make the configuration. 
For me the configuration tab was in the advanced networking mode. <br>
Here you need to add: <br>
<p class="message">
"Service Name" = ssh(22) <br>
"Action" = Allow <br>
"LAN IP Address" = IP address of your home machine <br>
"WAN IP Address" = Any (You can spcify the public IP of y our office network to be more secure) <br>
</p>

**DMZ**<br>
Demilitiarized Zone is a physical of logical sub-network that separates an internal local area network(LAN) from other untrusted networks, usually the Internet[http://searchsecurity.techtarget.com/definition/DMZ]. This means that the machines/servers in the DMZ are accessible from the outside network. To achieve our goal, instead of port forwarding, we can make you machine sit in the DMZ so that it will be publicly accessible. BUT, there is a big but here, as you might have guessed making your machine publicly avaible doesn't sound much secure. You are right. It would not be secure. Hence, let's stop this discussion here. <br>
But if anyone want to configure there machine to reside in the DMZ, you can do so by sepcifyinh your private IP into the router DMZ tab. After that the router will take care of it. (Again, I am assuming that your router supports DMZ setup)<br>

## Dynamic DNS
While performing port forwarding configuration when I say "IP address of your machine", you might question that my router leases IP using DHCP. Then how can I gurantee that every time I will have the same private IP adress? True. This can be a problem all the time. But, thanks to Dynamic DNS service. Dynamic DNS is a method of autmatically updating a name server in the DNS. So basically the only thing you have to understand is that it will provide you with a constant domain name for your local machine even though it will have different IP's. This can be configured on your router once you have the name configured using services like [noip](https://www.noip.com/free).

## SSH Reverse tunneling
In order to achieve the goal of bypassing corporate firewall, we use the technique of SSH Reverse Tunneling. Generally corporate firewalls are desgined to block any incoming connections from outside network. Also, for security purposes many social media websites are blocked on the firewall. But, many times a connection going from inside to outside is not blocked. Otherwise, it will be difficult to work. Right? 
Hence, we leverage this to our advantage and in this technique we try to open a connection from inside to outside.
In order to make a SSH reverse tunnel to your home PC use the below command: 
<p class="message">
ssh -R 4444:localhost:22 user@publicip
</p>
The -R option in above command will forward the give port on remote server to the given host and port on local side. In the above command, we use 4444 as the port on our home machine to connect back to our work machine. "user@publicip" means you are connecting to your home machine. 
Now, from your home machine you have to connect back to the office machine using the tunnel established. This time you will be able to connect because a legitimate port is open through the corporate firewall from inside to outside. 
<p class="message">
ssh -p 4444 user@localhost
</p>
This way you are connecting back to the work machine through the tunnel.
Now that the tunnel is established, in order to browse the blocked website we have to setup something called as SOCKS proxy on our browser. 
In order to do so, 
<p class="message">
open "Mozilla-firefox"<br>
go-to "preferences"<br>
click "advanced"<br>
"Network" > "Settings" > "SOCKS Host" > localhost: "Port" > 4444
</p>
Now all the traffice from this browser will get tunnel through the SSH reverse tunnel we established and will go via your home internet. 
This will enable us to access all the blocked websites with ease.

## SSH reverse tunneling technique is highly monitored in coportate networks. Your coporate IT team might not like it. Please think twice before performing this. I have written this blog post only to learn more about this technique. Hope this helps. :) :)



