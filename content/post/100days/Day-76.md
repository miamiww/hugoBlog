+++
title = "Shodan Stories Day 76: Conference Calls in Noida"
date = 2019-03-21T16:17:26-04:00
draft = false
tags = []
categories = ["100 days"]
+++

Today [I read about insecure video conferencing systems](https://www.rapid7.com/db/modules/exploit/unix/polycom_hdx_auth_bypass) made by [Polycom](https://www.polycom.com/), and Googled up a Shodan query to find them. The query was "polycom command shell".

## Polycom Conference Calling System on 14.143.72.118
The results were all video conferencing devices that had open telnet ports, but I ultimately chose one in India that was runnign a webserver as well, so that I could have something more interesting to take pictures of.

Checking the telnet port first:

```
👻🌵🔮 $ nc 14.143.72.118 23 -v
found 0 associations
found 1 connections:
     1: flags=82<CONNECTED,PREFERRED>
        outif ipsec0
        src 10.6.6.4 port 65263
        dst 14.143.72.118 port 23
        rank info not available
        TCP aux info available

Connection to 14.143.72.118 port 23 [tcp/telnet] succeeded!
!
Polycom Command Shell
XCOM host:    localhost port: 4121
TTY name:     /dev/pts/0
Session type: telnet
2019-03-21 20:32:58 DEBUG avc: pc[0]: XCOM:INFO:server_thread_handler: new conn [conn: 0x4c900468] [sock: 6] [thread: 0x11f71dc8] [TID: 3344]
2019-03-21 20:32:58 DEBUG avc: pc[0]: uimsg: [R: telnet /tmp/apiasynclisteners/psh0 /dev/pts/0]
2019-03-21 20:32:58 DEBUG avc: pc[0]: appcom: register_api_session pSession=0x13332088
2019-03-21 20:32:58 DEBUG avc: pc[0]: appcom: about to call sendJavaMessageEx
2019-03-21 20:32:58 DEBUG jvm: pc[0]: UI: xcom-api: ClientManager: createSession(type: telnet sess: 21617)
2019-03-21 20:32:58 DEBUG jvm: pc[0]: UI: xcom-api: ClientManager: createSession current open sessions count= 2
2019-03-21 20:32:58 DEBUG avc: pc[0]: appcom: session 21617 registered
```

I didn't want to spend a bunch of time figuring out how to look around here so I exited the connection and went to the webserver.

![](/images/100Days/Day76/firstlook.png)
I found pretty quickly that I could make any calls I wanted, see the entire call history, and even, maybe most troublingly, monitor any call in progress.
![](/images/100Days/Day76/recent.png)
A lot of the calls seemed to be within-network, which made me think that this could be an office's conference room phone for conference calling, as in my time in offices we'd frequently call a coworker mid-meeting to ask them some questions.
![](/images/100Days/Day76/monitor.png)
I don't understand not putting any password or authentication on this kind of system. I took a look at the security settings and it seems like they had chosen to set the security to "minimal". Why? I can't image that it was the default.

The last phone number called was an [Airtel India](https://www.airtel.in/) phone number, and I was tempted to call it so I could figure out whose phone I was looking at, but it seemed unwise and also too difficult. I hate phone calls. See you tomorrow.
