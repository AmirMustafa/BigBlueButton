# BigBlueButton
Linux - Video Conferencing system, includes presentation
Big Blue Button is basically used for a joint meeting for video conferencing system. For this is required a specific type of server. For proper installations and configuring follow below steps


## Minimum Requirements
- Ubuntu 16.04 64-bit OS   	- hostnamectl or cat /etc/os-release
- 4 GB of memory with swap enabled (8 GB of memory is better) - 19170240KB,  on file /dev/sda2, size 16777212, used 0, command – cat /proc/swaps or swapon -s
- Quad-core 2.6 GHZ CPU (or faster)  2.30GHz
- TCP ports 80, 443,and 1935 are accessible
- TCP port 7443 is accessible if you intend to configure SSL (recommended), otherwise port 5066 is accessible
- UDP ports 16384 - 32768 are accessible
- Port 80 is not in use by another application
- TCP ports 80, 443,and 1935 are accessible
- 500G of free disk space (or more) for recordings     - x (448GB free)      - df –h
- 100 Mbits/sec bandwidth (symmetrical)
- Dedicated (bare metal) hardware (optional)

## Installation

For this first login to putty(SSl command line) and hit cd / and follow below steps:
Login through putty and hit cd /
Execute all commands by root:
1.	sudo su root 
Now we will execute commands step by step:
2. grep "multiverse" /etc/apt/sources.list
3. echo "deb http://archive.ubuntu.com/ubuntu/ xenial multiverse" | sudo tee -a /etc/apt/sources.list
4. sudo apt-get update
5. sudo apt-get dist-upgrade
   Install apt-get key for BigBlueButton
6. wget https://ubuntu.bigbluebutton.org/repo/bigbluebutton.asc -O- |
7. sudo apt-key add –
8. sudo apt-get update
9. sudo apt-get install bigbluebutton
10. sudo bbb-conf –restart

<b>Assign the hostname</b><br>
This is the place where we are going to assign the domain name/ IP address where actual BigBlueButton will start
Now for this we have to check the IP via ping command whether it is running or not:
Eg. ping <domain/ip>
Eg2. ping demo.bigbluebutton.org
Eg3. ping 87.98.148.253 (it should return the address maybe non-stop)  conclusion           IP/domain works 
o/p: should have been like below
64 bytes from 146.20.105.32: icmp_seq=1 ttl=44 time=27.5 ms

Now below command will assign the BBB to that IP/domain
11. sudo bbb-conf --setip <ip/domain>
Eg. sudo bbb-conf --setip 87.98.148.253
Eg2. sudo bbb-conf --setip bbb.datarays.co
Now BigBlueButton is listening to this Domain/IP address and responding to this API requests.
<br>

<b>APP Secret Key</b><br>
This is important when some plugin is used in upon BBB eg. moodle mod plugin.<br>
12.	bbb-conf –secret
O/P:<br>
URL(BigBlueButton Server URL): http://87.98.148.253/bigbluebutton/
Secret (BigBlueButton Shared Secret):  831993ae09d236f75481530065ecc357

<br>

<b>Install API demos</b><br>
Here we install sample API demos<br>
13. Install: sudo apt-get install bbb-demo <br>
14. Remove: sudo apt-get purge bbb-demo 
<br>

<b>Install Client self-check</b><br>
Here we actually check the drivers of the BBB which are working. Note all should work in order to run video conferencing
15. Install: sudo apt-get install bbb-check
<br>
Link – website_assigned_hostname/check <br>
Eg. http://87.98.148.253/check/
16. Remove - sudo apt-get purge bbb-check

Some links for 1935 port in google groups:<br>
https://groups.google.com/forum/#!topic/bigbluebutton-setup/a7apCk2lxZw 
https://groups.google.com/forum/#!topic/bigbluebutton-setup/a7apCk2lxZw
https://groups.google.com/forum/#!topic/bigbluebutton-setup/qRHQQcqUERA
https://groups.google.com/forum/#!topic/bigbluebutton-setup/vGvOkDZ-v_8 

// works fine for the IP address
For checking the server:
18. sudo bbb-conf –check
<br>

<b>Ports used for this:</b><br><br>
<b>TCP PORTS</b><br>
80   – HTTP<br>
443  – HTTPS<br>
1935 – RTMP Port Video conferencing<br>
7443 – Audio<br><br>

<b>UDP PORTS</b><br>
clients must be able to connect on a port within the range 16384-32767 for WebRTC-based audio.<br>

Command to check port busy/free:
Netstat –anp|grep <port_number>
Eg. netstat -anp|grep 443

With BBB installed and hostname applied, the next steps are:<br>
(A) install the HTML5 client<br>
(B) configure BigBlueButton to work with your firewall (if needed)<br>
(C) configure SSL on your server (skip if you don’t have SSL at present)<br><br>


## (A) FIREWALL UBUNTU SETTINGS:
Link - https://help.ubuntu.com/lts/serverguide/firewall.html.en  
For Ubuntu firewall <br>
In putty root login run the following commands for all the ports<br>
19. sudo ufw allow <port_number><br>
o/p: <br>
Rules updated<br>
Rules updated (v6)<br>
i.e. for allowing the ports to pass the firewall:<br>
20. sudo ufw allow 80		HTTP Port<br>
21. sudo ufw allow 443		HTTPS Port<br>
22. sudo ufw allow 1935		RTMP  Port Video Conferencing<br>
23. sudo ufw allow 7443		Audio Port <br><br>

## (B)INSTALL THE HTML5 CLIENT:

Run the following commands:<br>
24. sudo apt-get update<br>
25. sudo apt-get dist-upgrade<br>
26. sudo apt-get install bbb-html5 (some warnings – meteor package install errors)<br>
27. sudo apt-get purge kms-core-6.0 kms-elements-6.0 kurento-media-server-6.0 (some warnings – meteor package install errors)<br>
<br><br>
Also, check the contents of /usr/local/bigbluebutton/bbb-webrtc-sfu/config/default.yml for the entry for kurentoUrl (it is near the top). If kurentoUrl has a wss in it, then<br>
28. kurentoUrl: wss://<server_name>/kurento<br>
<br><br>
Changed to<br>
ws://87.98.148.253:8888/kurento		(done)<br>
ws://bbb.datarays.co:8888/kurento<br>
Execute below command for the test<br>
29. sudo bbb-conf --setip 87.98.148.253<br><br>
Install api demos:<br>
30. sudo apt-get install bbb-demo	<br>

## INSTALL MONGODB AND NODEJS IN SERVER
BigBlueButton HTML5 client runs on Node JS server and MongoDB as db.<br>
31. sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6<br><br>

## MongoDB Installation:
32. echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list<br>

33. sudo apt-get update<br>
34. sudo apt-get install -y mongodb-org curl<br>
Next, the HTML5 client uses a nodeJS server to communicate with the BigBlueButton server.<br><br>

## Node JS Installation:
Check version of the node js:<br>
35. dpkg -l | grep nodejs<br>
<br>
We will uninstall node 4.x package and install node 8.x package as we see in screenshot<br>
36. curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -<br>
sudo apt-get install -y nodejs<br>
<br><br>
## Yarn Installation:
37. 
curl -sL https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -
     echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list
     sudo apt-get update && sudo apt-get install yarn<br>

38. sudo apt-get install -y bbb-html5<br>

The solution of 1935 port installation error is use IP of BBB server instead of pointed hostname domain<br>
39. sudo apt-get update<br>
40. sudo apt-get dist-upgrade<br>

Now we have to set the ip and port in WebRtcEndpoint.conf.ini page<br>
Path: /etc/kurento/modules/kurento/WebRtcEndpoint.conf.ini<br>
Open in vim/nano editor<br>
Remove ; from these two lines and add IP or hostname and port<br>
<br>
stunServerAddress = 87.98.148.253<br>
stunServerPort = 19302<br>

## Link to HTML5 client:
http://87.98.148.253/demo/demoHTML5.jsp 

## Test link from BBB site to see how BBB interface looks:
https://test.bigbluebutton.org/demo/demoHTML5.jsp


<br><br>
<b>Assign the hostname</b><br>
<br><br>

##Looks

![Screenshot of BooKart App](https://cloud.githubusercontent.com/assets/15896579/21071612/ce307c80-becb-11e6-9ea7-8464aef1e85d.PNG?raw=true "Screenshot of BooKart App")
<br/><br/><br/>

![Screenshot of BooKart App](https://cloud.githubusercontent.com/assets/15896579/21071613/ce5827a8-becb-11e6-9109-de309d5c130f.PNG?raw=true "Screenshot of BooKart App")
<br/><br/><br/>

![Screenshot of BooKart App](https://cloud.githubusercontent.com/assets/15896579/21071614/ce5f526c-becb-11e6-8da8-53a898fd4077.PNG?raw=true "Screenshot of BooKart App")
<br/><br/><br/>

![Screenshot of BooKart App](https://cloud.githubusercontent.com/assets/15896579/21071607/ce23a2a8-becb-11e6-84e5-a55334f3f57e.PNG?raw=true "Screenshot of BooKart App")
<br/><br/><br/>

<br/><br/><br/>

##Code Snippets

![Screenshot of BooKart's Code Snippets](https://cloud.githubusercontent.com/assets/15896579/21071608/ce2abd40-becb-11e6-8218-9bc9667be456.png?raw=true "Screenshot of BooKart's Code Snippets")
<br/><br/><br/>

![Screenshot of BooKart's Code Snippets](https://cloud.githubusercontent.com/assets/15896579/21071609/ce2b6a74-becb-11e6-8159-01a23072f41c.png?raw=true "Screenshot of BooKart's Code Snippets")
<br/><br/><br/>

![Screenshot of BooKart's Code Snippets](https://cloud.githubusercontent.com/assets/15896579/21071610/ce2c1ef6-becb-11e6-9272-fa44bfa3e5d5.png?raw=true "Screenshot of BooKart's Code Snippets")
<br/><br/><br/>

![Screenshot of BooKart's Code Snippets](https://cloud.githubusercontent.com/assets/15896579/21071611/ce2ce44e-becb-11e6-9850-348cfe9e7144.png?raw=true "Screenshot of BooKart's Code Snippets")
<br/><br/><br/>

## License

(The MIT License)

Copyright (c) 2016 Amir Mustafa

Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:

The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.


