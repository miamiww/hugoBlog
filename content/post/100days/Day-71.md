+++
title = "Shodan Stories Day 71: Transfering Files in Moscow, Macommet, and Open Source Mirrors"
date = 2019-03-15T22:13:53-04:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I just wanted to find a working public FTP server. So I searched "FTP", and went with the first result I found, this one in Moscow.

## FTP Server on 195.128.64.25
[FTP](https://en.wikipedia.org/wiki/File_Transfer_Protocol) seems like an ancient technology but I had a job just a few years ago where we would use it all of the time, and I frequently use it to move files to my servers when I can't be bothered to remember the correct [scp](https://en.wikipedia.org/wiki/Secure_copy) syntax. It turns out though that the newest Mac operating systems took out FTP from the built in software, so I had to reinstall it. They still have SFTP, which is the preferable protocol to use anyway, but since SFTP and FTP aren't actually interoperable, I needed the original model.

```
👻🌵🔮 $ ftp -n 195.128.64.25
Connected to 195.128.64.25.
220 FTP server ready.
ftp> user
(username) anonymous
331 Guest login ok, send your email address as password.
Password:
230-
230-   _ __ ___   __ _  ___ ___  _ __ ___  _ __   ___| |
230-  | '_ ` _ \ / _` |/ __/ _ \| '_ ` _ \| '_ \ / _ \ __|
230-  | | | | | | (_| | (_| (_) | | | | | | | | |  __/ |
230-  |_| |_| |_|\__,_|\___\___/|_| |_| |_|_| |_|\___|\__|
230-
230-
230- The FTP archive at MAcomnet, Moscow, Russia.
230-
230- All the equipment including 1Gbps connection provided by
230- MAcomnet JSC, http://www.macomnet.ru/.
230-
230- This archive is available via
230-
230- HTTP:   http://mirror.macomnet.net/     (max 1024 connections)
230- FTP:    ftp://mirror.macomnet.net/      (max 1024 connections)
230- RSYNC:  rsync://mirror.macomnet.net/    (max 30 connections)
230-
230- Please email comments, bug reports and requests for packages to be
230- mirrored to mirror@macomnet.net
230 Guest login ok, access restrictions apply.
ftp>
```
Here is my amazing result after connecting (via port 21, the typical FTP port). Now oddly I couldn't get that much done, my list of commands seemed to be severely restricted as an anonymous user, I couldn't even use `ls`. So I instead opted to look around via the browser FTP protocol. First though I double checked that indeed the IP I had was the same URL that the FTP header above was directing me toward.
```
👻🌵🔮 $ host 195.128.64.25
25.64.128.195.in-addr.arpa domain name pointer mirror.macomnet.NET.
```
Yup we are all good. Wait actually let's first see what macommet is.

![](/images/100Days/Day71/macommet.png)
Great it's a Russian telecom, but why are they running an FTP server? Let's take a look.
![](/images/100Days/Day71/firstlook.png)
I'm guessing from the timestamps that this server was set up back in 2008 but is still being used as of a couple of days ago. Now /bin/ and /etc/ are just where all of the commands you can use when logged into the server are. /pub/ is where all the good stuff is.
![](/images/100Days/Day71/pub.png)
It's a bunch of open source software! Kind of an amazing little collection actually. There's [CTAN](https://ctan.org/?lang=en) and [lyx](https://en.wikipedia.org/wiki/LyX) for your word processing, two kinds of [BSD](https://en.wikipedia.org/wiki/FreeBSD) operating systems, [Hiren's BootCD](https://www.hirensbootcd.org/) for your hard drive backups, and the classic [VLC](https://www.videolan.org/vlc/index.html).

After wondering why this telecom had done this for a bit I noticed something I had missed before. The url had "mirror" in it! Of course, they were putting up open source software on an FTP server to help [spread access to the software and share bandwidth loads](https://en.wikipedia.org/wiki/Mirror_website) with the open source projects, so that they wouldn't have to bear the cost of heavy download traffic themselves. This used to be more common, but bandwidth has gotten cheaper these days, you don't need so much community support like this anymore. Or maybe mirroring is still a big deal and I've just gravitated away from the world of downloading a lot of open source software, with my Mac operating system that doesn't even have FTP.

See you tomorrow.
