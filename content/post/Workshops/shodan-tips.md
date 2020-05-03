+++
title = "Shodan Workshop Resource List"
date = 2019-06-13T16:19:25-04:00
draft = false
tags = []
categories = ["workshops"]
+++

[![](https://accelerator-origin.kkomando.com/wp-content/uploads/2017/10/hacker.jpg)](https://www.youtube.com/watch?v=K7Hn1rPQouU)

Welcome! This is a list of resources to supplement my "Basic Hacking in 2019 with Shodan" workshop.

First it's very important to take care of yourself out there when you start poking around. I recommend a VPN to hide who you are a bit and some kind of browser tools to prevent someone from running malicious code in your browser.

My favorite VPN is [Nord](https://nordvpn.com/), and I use the [uMatrix](https://github.com/gorhill/uMatrix) browser extension in all my browsers to control what code my browsers are running.

## Online Tools

* [Shodan](https://www.shodan.io/) - search engine for anything connected to the internet!
* [PublicWWW](https://publicwww.com/) - search engine for websites' source code!
* [Wigle](https://wigle.net/) - search engine for wifi networks!

## Command Line Tools

* `host` - gives you the IP address of any domain name by querring your [DNS of choice](https://www.cloudflare.com/learning/dns/what-is-dns/)

* `whois` - queries the [WhoIs database](https://whois.icann.org/en) to get a variety of information about a domain or IP address

* `nslookup` - similar to `host`

* `ping` - sends packets to an address to see if you get a response, good for checking if a host is up

* `nc` - known as "[netcat](http://netcat.sourceforge.net/)", swiss army knife of creating network connections

* `telnet` - can create a tcp connection between you and someone else, very insecure and now almost entirely replaced by `nc`

* `traceroute` - prints every server between you and a desired address
* `nmap` - a powerful and dangerous port scanner [read more here](https://nmap.org/)

* `ssh` - create a secure shell connection, a way of logging into a remote computer over the command line
* `ftp` - file transfer protocol, method of transfering files

## GUI Software
* [Wireshark](https://www.wireshark.org/) - packet sniffing tool
* [Herbivore](https://github.com/samatt/herbivore) - simpler but buggy packet sniffer
* [VNC Viewer](https://www.realvnc.com/en/connect/download/viewer/) - way of connecting to [VNC servers](https://en.wikipedia.org/wiki/Virtual_Network_Computings)
