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
(A) configure SSL on your server (skip if you don’t have SSL at present)<br>
(B) configure BigBlueButton to work with your firewall (if needed)<br>
(C) install the HTML5 client<br><br>




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


