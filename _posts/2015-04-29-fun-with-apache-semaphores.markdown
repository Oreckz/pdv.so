---
layout: post
title: Fun with Apache Semaphores
quote: Because who needs useful error messages?
date:  2015-04-29T15:33
---

Every so often I come across a problem that truly leaves me stumped. The following issue had me scratching my head for a good forty-five minutes, might not sound like a long 
time but when uptime is critical 45 minutes is an eternity. 

So where do we go when a process crashes with no errors and refuses to start without showing any? According to a far more experienced colleague of mine we check the Kernel.
Makes sense right? This isn't a programming blog so I won't be going deep into semaphores and theory but suffice to say if a process has stopped but is still showing
semaphores in the kernel it isn't a good thing. 

We can check the semaphores for a given process like so:
`ipcs -s | grep apache`

Or whichever process you would like to check.

On seeing that this showed active counters I came up with the following to remove them:
```
for i in `ipcs -s | grep apache | awk '{ print $2 }'` ; do ipcrm -s $i ; done;
```

After running the above I was able to start Apache from the init script, bring things back online and make everyone happy. If you'd like to read more on semaphores you can
do so [here](http://archive.oreilly.com/pub/a/linux/2007/05/24/semaphores-in-linux.html) or Google it. Whatever.
