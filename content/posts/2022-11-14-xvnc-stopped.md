---
title: xvnc stopped
date: 2022-11-14 17:51:42
tags:
  - vnc
  - rhel
category: notes
keywords:
  - tigervnc-server
  - vnc
  - rhel
  - Red Hat
  - rhel 5.11
  - vnc server
---

after few days of waiting for installers from our supplier

I finally got the chance to install customize rhel 5.11 on a workstation

but when I tried to start vnc server

it **failed**

```
VNC server: [FAILED]
```

but thanks to google and stackoverflow

I found the solution

> removing the file _X1_ via `rm -f /tmp/.X11-unix/X1` and restarting VNC server worked
>
> > [yildizabdullah](https://serverfault.com/questions/925061/unable-to-start-vnc-server-configured-resource-limit-was-exceeded)

```
[root@localhost ~]# rm -f /tmp/.X11-unix/X1

```

and then restart vnc server

```
[root@localhost ~]# service vncserver start

Starting VNC server: [  OK  ]

```

The problem is **solved** :)
