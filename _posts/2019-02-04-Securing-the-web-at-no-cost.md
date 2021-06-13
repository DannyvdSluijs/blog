---
title: 'Securing the web at no cost'
date: 2019-02-04 21:20:27
tags:
---
# Securing the web at no cost
For work stuff some time ago, I've been working on the SSL setup which has triggered me to see if I could start securing my personal website. Because obviously I'm a very hacker rich target ;-). But since I don't make any money from that, why should I even spend a dime on a secure website. Well because you can do it for **FREE**. Even the time you'll need to invest is minimal. 

_Disclaimer: This post works on the assumption you're having root access to your server and it runs a Ubuntu 18.04 with Apache setup_

# Getting an SSL certificate
Due to the fine folks of [Let's Encrypt](https://letsencrypt.org/getting-started/) and their certbot software getting (and installing) a certificate because supper easy. All you need is to open up a terminal and execute the following commands:
```bash
$ sudo apt-get update
$ sudo apt-get install software-properties-common
$ sudo add-apt-repository universe
$ sudo add-apt-repository ppa:certbot/certbot
$ sudo apt-get update
$ sudo apt-get install certbot python-certbot-apache
$ sudo certbot --apache
```
This will handle all the _"difficult stuff"_ such as the generating of a Certificate Signing Request, retrieving the certificate and even adjusting your apache setup. The only manual steps required is some interactive selection of which enabled sites should get a certificate. In order to skip the automatic configuration of Apache `certonly` can be added as a command argument.

Now your site should be available on HTTPS. If it fails you might want to check your firewall to see if HTTPS (Port 443) is allowed. You can put your HTTPS setup to the test at [SSL Labs](https://www.ssllabs.com/ssltest/) 

# Security headers
After validating my HTTPS setup from the previous step, I started to wonder if some more security setup could be done. Using the website [https://securityheaders.com](https://securityheaders.com), I was able to find that I was basically missing all the headers I could think of. Using their website, was quite easy to determine which headers to add to the Apache sites
 
```apacheconfig
Header always set Strict-Transport-Security "max-age=63072000; includeSubDomains"
Header always set X-Frame-Options "SAMEORIGIN"
Header always set X-Xss-Protection "1; mode=block"
Header always set X-Content-Type-Options "nosniff"
Header always set Referrer-Policy: "no-referrer-when-downgrade"
Header always set Feature-Policy "geolocation none;midi none;notifications none;push none;sync-xhr none;microphone none;camera none;magnetometer none;gyroscope none;speaker self;vibrate none;fullscreen self;payment none;"
Header always set Content-Security-Policy "script-src 'self'"
```

Just by reading the linked articles on each individual _"missing"_ header I have gotten to know a bit more about the headers that are involved with the securing of a website. Some tweaking of the headers might be needed as your setup might differ.

# Goal achieved?
All in all, I've spent a total of 30 minutes and € 0,00 to secure my site with an SSL certificate and even added some security headers whilst I was at it. Obviously when doing this for any web application which uses any form of customer data more time should be spent in getting your security setup. For my personal web space this was sufficient.  