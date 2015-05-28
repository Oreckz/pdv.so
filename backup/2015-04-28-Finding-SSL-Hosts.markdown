---
layout: post
title:  "Finding SSL Hosts"
date:   2015-04-28 17:26
categories: general
---

RHEL/CentOS
```
httpd -S 2>&1|grep "port 443 name"|grep -v `hostname`| awk {'print $4'}
```
Debian/Ubuntu
```
apache2ctl -S 2>&1|grep "port 443 name"|grep -v `hostname`| awk {'print $4'}
```

I cobbled these two one liners together for use in-house during the advent of
the now well known Heartbleed OpenSSL bug. Each command will return the hostnames
of all sites using SSL/TLS certificates on the server. This was necessary as many
customers required their certificates to be regenerated following the incident. 
