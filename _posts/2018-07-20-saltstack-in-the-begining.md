---
layout: post
published: false
title: SaltStack - In the begining
---
![Waving hand in the ocean - photo by Mishal Ibrahim]({{site.baseurl}}/img/mishal-ibrahim-615607-unsplash.jpg)


In the begining, I had attended the OSS Summit and achieved a level of enlightenment from a talk by @supertylerc. The subject was Network Automation. His demostration provided the use of Saltstack, proxy minions and some networking devices and how after taking a port down, managed to get the OSPF matric changed almost instantly.

Since then, I have trying to find the time to create a simplistic lab with a Salt-Master, Salt-Minion & Salt-Proxy. I have a test Cisco 3560 as1.test running a recent version of ios and Cisco ASR903 pe1.test running a recent version of ios-xe.

So after defining my pillar_roots on my master, I have created a top.sls file & a as1.test.sls file in the pillar_roots.

so... top.sls

``` 
base:
  'as1.test':
    - as1_test
  'pe1.test':
    - pe1_test
```

as1_test.sls

```
proxy:
  proxytype: napalm
  driver: ios
  host: as1.test
  username: mcparty
  passwd: WordUp
```

There is a lot of talk about Cisco devices but it took 6 hours of searching to find that if you are using ios-xe you can use the NAPALM ios driver.

pe1_test.sls

```
proxy:
  proxytype: napalm
  driver: ios
  host: pe1.test
  username: mcparty
  passwd: WordUp
  
```


#NAPALM#

In a nutshell NAPALM is a python library which you can query without the use of Saltstack which is a good troubleshooting tool. To install, use pip. Though NAPALM comes fully integrated with NAPALM so you shouldn't need to do the following, but i did... and this broke me slowly as I couldn't install NAPALM due to a silly firewall issue that had me sobbing gently for a few hours as I am no Python expert and the sight of lots of Traceback errors had me frantically searching the Internet for a solution. So, i'll make this bold: **Check your firewall settings** 

```apt install pip

pip install napalm
```


