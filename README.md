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


## (C)SSL Changes:
For SSL following steps needs to be done:<br>
Suppose you receive SSL bundle from any Certificate Authoity (CA) Eg. GeoTrust, Commodo etc.<br>
1.	You should have received following files:<br>
a.	Certificate (.crt  or .cer )<br>
b.	Intermediate Certificates(if any) (.crt or .cer)<br>
c.	Private Key +Certificate Signing Request (CSR) (this must be received in the file or in the server)<br>
Eg. check in the path /home/usr in your server path<br>

Eg. server.csr and server.key file<br>

If somehow you are getting you received empty .key file i.e. 0<br>
Then you have to resubmit the CSR and receive new Certificate.<br>

2.	Basically means with the help of openssl command, generate new CSR and new Private key, and that CSR must be submitted from your SSL Authority Account(eg. GeoTrust)<br>

openssl req -new -key domainname.key -out domainname.csr<br>

Note each time you hit this command in SSH, it will generate new CSR and private key<br>
Therefore hit this command once and submit this latest CSR<br>

Login  Reissue  in the input box paste the CSR new generated and submit it.<br>

At the same time you can contact their support live chat and update them about new CSR, so that they can reissue new certificate (via download link)<br>

Once you receive proper certificate and its equivalent private key.<br>

You have to merge all the certificate and intermediate certificates in one file.<br><br>

For GeoTrust, it should be in .pem format
cat your_domain.crt intermediate.crt root.crt >> ssl-bundle.crt
So inside .pem (eg. ssl_bundel.pem) file it have first main certificate, then intermediates certificate pasted
<br>
Sample Certificate
<br>
-----BEGIN CERTIFICATE-----<br>
MIIFtjCCBJ6gAwIBAgIQA7nqAmHvlPhdaj3rsDXrZTANBgkqhkiG9w0BAQsFADBe
MQswCQYDVQQGEwJVUzEVMBMGA1UEChMMRGlnaUNlcnQgSW5jMRkwFwYDVQQLExB3
d3cuZGlnaWNlcnQuY29tMR0wGwYDVQQDExRHZW9UcnVzdCBSU0EgQ0EgMjAxODAe
Fw0xODA3MjcwMDAwMDBaFw0xOTA3MjMxMjAwMDBaMB8xHTAbBgNVBAMTFGJiYi5k
YXRhcmF5c2FwcHMuY2wewwewIjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA
zqAJC9pNaeCseTH8QQqpxFdmduTfXjpdjJT/g5flM5n8D9YBdUeO9R962PRQnBRK
dBHrvLl8yp/J7UIDN7xCrOlmwYDHucNyWSdKn87pDXQF4jCkG+HT/Z9OYnKwc6Zt
6ojYWpe1RhOZm4u8FRdcfmbd92Fa3w0XQU6jaZq5Yfzv5DceOmw/Bg2za8VGczs9
ga9yTZkL+EJXzcZ7zBDvM/hf8HcusvNQgj2L5RZnDtC/F57jGfVhmCnoHkIdgaiI
Um+kKvVp33JNpQvt0Zg0b7Cv/rgbsQ7jVpDSZ1n2mQlVEmpmw4VICADlRuNJHX7x
qWb+fXMV254xtszqRH5JmQIDAQABo4ICrTCCAqkwHwYDVR0jBBgwFoAUkFj/sJx1
qFFUd7Ht8qNDFjiebMUwHQYDVR0OBBYEFEqvfyeJECp0WuNMUaUJtbiOWDrfMB8G
A1UdEQQYMBaCFGJiYi5kYXRhcmF5c2FwcHMuY29tMA4GA1UdDwEB/wQEAwIFoDAd
BgNVHSUEFjAUBggrBgEFBQcDAQYIKwYBBQUHAwIwPgYDVR0fBDcwNTAzoDGgL4Yt
aHR0cDovL2NkcC5nZW90cnVzdC5jb20vR2VvVHJ1c3RSU0FDQTIwMTguY3JsMEwG
A1UdIARFMEMwNwYJYIZIAYb9bAECMCowKAYIKwYBBQUHAgEWHGh0dHBzOi8vd3d3
LmRpZ2ljZXJ0LmNvbS9DUFMwCAYGZ4EMAQIBMHUGCCsGAQUFBwEBBGkwZzAmBggr
BgEFBQcwAYYaaHR0cDovL3N0YXR1cy5nZW90cnVzdC5jb20wPQYIKwYBBQUHMAKG
MWh0dHA6Ly9jYWNlcnRzLmdlb3RydXN0LmNvbS9HZW9UcnVzdFJTQUNBMjAxOC5j
cnQwCQYDVR0TBAIwADCCAQUGCisGAQQB1nkCBAIEgfYEgfMA8QB3AKS5CZC0GFgU
h7sTosxncAo8NZgE+RvfuON3zQ7IDdwQAAABZNpdK8IAAAQDAEgwRgIhAOlid6yu
ZHcAjtYMEmHNoHehs7PxM0y2c6ASPJ+xnWbbAiEA1KrE/aX0YvdCMwNc6ffhtang
3kkN7KYbM4BuaYZI4JEAdgCHdb/nWXz4jEOZX73zbv9WjUdWNv9KtWDBtOr/XqCD
DwAAAWTaXSyYAAAEAwBHMEUCIQDxQwP63bH5oC64hRtbj2OO6eB/VQ8KqrqWeDhZ
PhzK3wIgK0SFugptCsGMEoHwAOADAfNJcyHxWyUQ5b3J0GeQOIowDQYJKoZIhvcN
AQELBQADggEBAIZH/9CZuFUr+1/ebTYEhQIy9ev7+wSIA29tqhi7Nm12EJ1Qdmok
U7kNDm9QvzCevGWaxuRl1fafcOWG0LoQOi3Xpqx1leAhOUrAKad2XeuiR2B2NbF1
Az61ZEvwKQsc55qQ4gYLOhCpImiqEoLSgyfVPqa1szWnX4lS8uplKzJdjzXATJu3
4+yJsuOqFU4w6xio0SisQVE6EfLF/HB+7q5vIsa8t+yjzyrGIYjW5bMqPzpcqtgx
WcreHLm909aAm0q3kR+7OjzSgiWRZgFc4IdRZcJUYZMGFS6Sn/4Tz1p4g3eRM1Md
zxVQ1pYwpYnxnlMpjunj6O39IkJ5cROl8MU=<br>
-----END CERTIFICATE-----<br>
-----BEGIN CERTIFICATE-----<br>
MIIEizCCA3OgAwIBAgIQBUb+GCP34ZQdo5/OFMRhczANBgkqhkiG9w0BAQsFADBh
MQswCQYDVQQGEwJVUzEVMBMGA1UEChMMRGlnaUNlcnQgSW5jMRkwFwYDVQQLExB3
d3cuZGlnaWNlcnQuY29tMSAwHgYDVQQDExdEaWdpQ2VydCBHbG9iYWwgUm9vdCBD
QTAeFw0xNzExMDYxMjIzNDVaFw0yNzExMDYxMjIzNDVaMF4xCzAJBgNVBAYTAlVT
MRUwEwYDVQQKEwxEaWdpQ2VydCBJbmMxGTAXBgNVBAsTEHd3dy5kaWdpY2VydC5j
b20xHTAbBgNVBAMTFEdlb1RydXN0IFJTQSBDQSAyMDE4MIIBIjANBgkqhkiG9w0B
AQEFAAOCAQ8AMIIBCgKCAQEAv4rRY03hGOqHXegWPI9/tr6HFzekDPgxP59FVEAh
150Hm8oDI0q9m+2FAmM/n4W57Cjv8oYi2/hNVEHFtEJ/zzMXAQ6CkFLTxzSkwaEB
2jKgQK0fWeQz/KDDlqxobNPomXOMJhB3y7c/OTLo0lko7geG4gk7hfiqafapa59Y
rXLIW4dmrgjgdPstU0Nigz2PhUwRl9we/FAwuIMIMl5cXMThdSBK66XWdS3cLX18
4ND+fHWhTkAChJrZDVouoKzzNYoq6tZaWmyOLKv23v14RyZ5eqoi6qnmcRID0/i6
U9J5nL1krPYbY7tNjzgC+PBXXcWqJVoMXcUw/iBTGWzpwwIDAQABo4IBQDCCATww
HQYDVR0OBBYEFJBY/7CcdahRVHex7fKjQxY4nmzFMB8GA1UdIwQYMBaAFAPeUDVW
0Uy7ZvCj4hsbw5eyPdFVMA4GA1UdDwEB/wQEAwIBhjAdBgNVHSUEFjAUBggrBgEF
BQcDAQYIKwYBBQUHAwIwEgYDVR0TAQH/BAgwBgEB/wIBADA0BggrBgEFBQcBAQQo
MCYwJAYIKwYBBQUHMAGGGGh0dHA6Ly9vY3NwLmRpZ2ljZXJ0LmNvbTBCBgNVHR8E
OzA5MDegNaAzhjFodHRwOi8vY3JsMy5kaWdpY2VydC5jb20vRGlnaUNlcnRHbG9i
YWxSb290Q0EuY3JsMD0GA1UdIAQ2MDQwMgYEVR0gADAqMCgGCCsGAQUFBwIBFhxo
dHRwczovL3d3dy5kaWdpY2VydC5jb20vQ1BTMA0GCSqGSIb3DQEBCwUAA4IBAQAw
8YdVPYQI/C5earp80sdsdsweAtpdiXft9OlWwJLwKlUtRfccKj8QW/Pp4b7h6QAl
ufejwQMb455OjpIbCZVS+awY/R8pAYsXCnM09GcSVe4ivMswyoCZP/vPEn/LPRhH
hdgUPk8MlD979RGoUWz7qGAwqJChi28uRds3thx+vRZZIbEyZ62No0tJPzsSGSz8
nQ//jP8BIwrzBAUH5WcBAbmvgWfrKcuv+PyGPqRcc4T55TlzrBnzAzZ3oClo9fTv
O9PuiHMKrC6V6mgi0s2sa/gbXlPCD9Z24XUMxJElwIVTDuKB0Q4YMMlnpN/QChJ4
B0AFsQ+DU0NCO+f78Xf7<br>
-----END CERTIFICATE-----<br>

<br>
After this restart your nginx to reflect intermediate certificate 
<br>
sudo service nginx restart
<br>
3.	Now you have to create directory in your server named ssl like below
/etc/nginx/ssl
<br>
Paste all the certificate ssl_bundel.pem (certificate), server.key (private key file)<br>
 
4.	You will have to generate a set of 2048-bit diffie-hellman now using below command <br>

Note :- enter this command when you are present in "SSL" directory<br>

openssl dhparam -out /etc/nginx/ssl/dhp-2048.pem 2048 <br>
So this command will generate dhp-2048.pem file inside ssl directory<br>

5.	Now before editing server files one last step we need to do is to check if your domain’s certificate is set up properly. 
For this we have a website which checks grade on entering URL<br>

Link - https://dev.ssllabs.com/ssltest/analyze.html?d=bbb.dataraysapps.com&hideResults=on <br>

Grade must be A on result. If grade of your website is coming B, it means intermediate certificates are not installed properly. Check with you Certificate Authority support for proper guidance<br>


6.	Now edit the following file in SSH:<br>
We will give path to all the files generated above plus set server configuration for SSL i.e. 443 port<br>

sudo vi /etc/nginx/sites-available/bigbluebutton<br>


server {<br>
  server_name www.example.com;<br>
  listen 80;<br>
  listen [::]:80;<br>
  listen 443 ssl;<br>
  listen [::]:443 ssl;<br>
  ssl_certificate /etc/nginx/ssl/ssl_bundel.pem;<br>
  ssl_certificate_key /etc/nginx/ssl/server.key;<br>
  ssl_session_cache shared:SSL:10m;<br>
  ssl_session_timeout 10m;<br>
  ssl_protocols TLSv1 TLSv1.1 TLSv1.2;<br>
  ssl_ciphers "ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:ECDH+3DES:DH+3DES:RSA+AESGCM:RSA+AES:RSA+3DES:!aNULL:!MD5:!DSS:!AES256";<br>
  ssl_prefer_server_ciphers on;<br>

  ssl_dhparam /etc/nginx/ssl/dhp-2048.pem;<br>

7.	Next step is to configure Free Switch for SSL:<br>

a.	Edit following file in SSH:<br>

vim /opt/freeswitch/etc/freeswitch/sip_profiles/external.xml<br>

Search for ws-binding line:<br>
<param name="ws-binding" value=":5066"/><br>
Replace that line with below line<br>
<param name="wss-binding" value=":7443"/><br>

b.	Edit sip.nginx file like below:<br>
vim /etc/bigbluebutton/nginx/sip.nginx<br>

location /ws {<br>
  proxy_pass https://203.0.113.1:7443;<br>
     proxy_http_version 1.1;<br>
  proxy_set_header Upgrade $http_upgrade;<br>
     proxy_set_header Connection "Upgrade";<br>
     proxy_read_timeout 6h;<br>
proxy_send_timeout 6h;<br>
client_body_timeout 6h;<br>
send_timeout 6h;<br>
}<br>
8.	Configure BigBlueButton to load session via HTTPS<br>

vim /var/lib/tomcat7/webapps/bigbluebutton/WEB-INF/classes/bigbluebutton.properties<br>

search for below line:<br>

bigbluebutton.web.serverURL=http://bigbluebutton.example.com<br>

Replace link like below:<br>

bigbluebutton.web.serverURL=https://bigbluebutton.example.com<br>

9.	Now edit screenshare properties:<br>

vim /usr/share/red5/webapps/screenshare/WEB-INF/screenshare.properties<br>

We will change jnlpUrl  and jnlpFile to HTTPS like below:<br>

jnlpUrl=https://bigbluebutton.example.com/screenshare<br>
jnlpFile=https://bigbluebutton.example.com/screenshare/screenshare.jnlp<br>

10.	Next step is to update the config.xml file<br>
Path - /var/www/bigbluebutton/client/conf/config.xml<br> 

This can be updated with the help of the single command<br>

http to https:<br>
sed -e 's|http://|https://|g' -i /var/www/bigbluebutton/client/conf/config.xml<br>

Suppose revert for any reason i.e. https to http:<br>
sed -e 's|https://|http://|g' -i /var/www/bigbluebutton/client/conf/config.xml<br>

11.	Next, modify the creation of recordings so they are served via HTTPS. <br>
Edit /usr/local/bigbluebutton/core/scripts/bigbluebutton.yml and change the value for playback_protocol as follows:<br>
vim /usr/local/bigbluebutton/core/scripts/bigbluebutton.yml<br>
search for:<br>
playback_protocol: http<br>

replace with:<br>
playback_protocol: https<br>

12.	If you have installed the API demos in step 4, <br>
Edit /var/lib/tomcat7/webapps/demo/bbb_api_conf.jsp and change the value of BigBlueButtonURL use HTTPS as done below:<br>
vim /var/lib/tomcat7/webapps/demo/bbb_api_conf.jsp<br>

Search for:<br>
String BigBlueButtonURL = "http://bigbluebutton.example.com/bigbluebutton/";<br>
Replace with:<br>
String BigBlueButtonURL = "https://bigbluebutton.example.com/bigbluebutton/";<br>

13.	Finally, to apply all of the configuration changes made, you must restart all components of BigBlueButton:<br>
bbb-conf --restart<br>
14.	Path to check the salt.<br>
Generally if server/ domain change happens too many time. In might happen the salt in the .jsp file does not change<br>

For this you have to two things need to be done:<br>
a.	In SSH hit bbb-secret<br>
This will display:<br>
URL and Secret Key<br>
In .jsp file  edit /var/lib/tomcat7/webapps/demo/bbb_api_conf.jsp<br>
Sudo vim /var/lib/tomcat7/webapps/demo/bbb_api_conf.jsp<br>
See the url and secret key both must match exactly<br>

Now we have to  restart the tomcat:<br>
sudo service tomcat7 restart<br>

Now try to run the domain name- it should work properly.<br>

##Looks

![Screenshot of BigBlueButton 1st Page](https://user-images.githubusercontent.com/15896579/44000534-3be2c3b0-9e3f-11e8-9c22-e58576c05b6c.png?raw=true "BigBlueButton 1st Page")
<br/><br/><br/>

![Screenshot of BigBlueButton Loader](https://user-images.githubusercontent.com/15896579/44000535-3c0e16aa-9e3f-11e8-8f5b-6a5563671254.png?raw=true "BigBlueButton Loader")
<br/><br/><br/>

![Screenshot of BigBlueButton Action select](https://user-images.githubusercontent.com/15896579/44000536-3c37d0ee-9e3f-11e8-8d8e-284152093cd8.png?raw=true "Screenshot of BigBlueButton Action select")
<br/><br/><br/>

![Screenshot of BigBlueButton Main Page](https://user-images.githubusercontent.com/15896579/44000537-3c616f80-9e3f-11e8-969a-dade70dcc16a.png?raw=true "Screenshot of BigBlueButton Main Page")
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


