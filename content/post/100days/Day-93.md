+++
title = "Shodan Stories Day 93: Poking the BusyBox in Camboriu"
date = 2019-04-12T22:22:42-04:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I saw someone's search for [BusyBox's](https://busybox.net/), the query was "port:9000 ash". BusyBox is a kind of GNU-lite system for embedded boards, allowing you to telnet into a shell that has most of the usual tools you get in Linux. It seems like it gets used in modems and stuff.

## A BusyBox on 191.186.195.10
I picked the very first result, in Brazil. So it's not very interesting in some senses, it's just running a telnet port on 9000. But you can connect and look around and stuff. It's all read-only. Trying to figure out what it was exactly got me on this [Russian linux forum](https://rdot.org/forum/archive/index.php/t-6-p-14.html) which is really not where I want to be.

See you tomorrow.
