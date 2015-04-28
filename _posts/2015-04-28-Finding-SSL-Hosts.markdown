---
layout: post
title:  "Finding SSL Hosts"
date:   2015-04-28 17:26
categories: general
---

RHEL/CentOS
```bash
httpd -S 2>&1|grep "port 443 name"|grep -v `hostname`| awk {'print $4'}
```
Debian/Ubuntu
```bash
apache2ctl -S 2>&1|grep "port 443 name"|grep -v `hostname`| awk {'print $4'}
```
