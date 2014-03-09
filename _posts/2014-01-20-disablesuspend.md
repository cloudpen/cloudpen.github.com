---
title: How to disable Suspend when close the lid
layout: post
category: Linux
---

When we close the lid, the system would auto suspend. But, sometimes, auto suspend is one of the most hated thing. So how to disable it?

There are many ways to do, but not cure. So, you can try the following mdthod.It's so simple.

Type this in terminal:

    sudo vim /etc/systemd/logind.conf

Then search for "#HandleLidSwitch=suspend"

To modify this text into

    HandleLidSwitch=ignore

At last, save the file and restart systemd-logind.
