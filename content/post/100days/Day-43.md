+++
title = "Shodan Stories Day 43: Jamming Out in Centerville, Bundesliga Fans, and the Discreet Charm of the Presentation Page"
date = 2019-02-15T21:50:06-05:00
draft = false
tags = []
categories = ["100 days"]
+++

I decided to double dip on AV receivers since someone was going so deep on them the past few days. Today I decided to look at [Pioneer](https://www.pioneerelectronics.com/PUSA/).

## Pioneer AV Receiver on 167.142.82.87
I mostly know pioneer as a manufacturer of [CDJs](https://www.pioneerdj.com/en-us/product/player/cdj-2000nxs2/black/overview/), and had no idea that they had a diverse product line beyond DJ equipment. They make bike equipment and accessories, a wide variety of audio equipment, and some kinds of computer electronics. I found a Pioneer AV receiver in Ohio, in a small town just north of Cincinnati, Shodan indicated it was just running a webserver on port 80.
![](/images/100Days/Day43/firstlook.png)
Nothing too interesting, although they named the device [Eintracht Frankfurt](https://en.wikipedia.org/wiki/Eintracht_Frankfurt), I assume after the German soccer team. There is a link to the owner's Pandora account but it's through a login. However there is the option to upload the firmware, a pretty damming security hole. I also found that this is a VSX-1023 model.
![](/images/100Days/Day43/vsx.png)
Looks like it's still made! You can buy one for just $400

I decided to check on `nmap`
```
👻🌵🔮 $ nmap 167.142.82.87
Starting Nmap 7.70 ( https://nmap.org ) at 2019-02-15 22:13 EST
Stats: 0:00:02 elapsed; 0 hosts completed (1 up), 1 undergoing Connect Scan
Nmap scan report for blfd-4-167-142-82-87.dsl.netins.net (167.142.82.87)
Host is up (0.066s latency).
Not shown: 995 closed ports
PORT     STATE SERVICE
80/tcp   open  http
443/tcp  open  https
1024/tcp open  kdm
1900/tcp open  upnp
8080/tcp open  http-proxy

Nmap done: 1 IP address (1 host up) scanned in 78.23 seconds
```

The https page isn't actually showing anything and 1024 is Apple Play again. 1900 is probably for integration with miscellaneous types of media services.

Shockingly though, and truly inexplicable for me, the 8080 port is running the exact same webservice as the Yamaha device from yesterday.
![](/images/100Days/Day43/presentation.png)
PRESENTATION PAGE. Again! These are from different manufacturers! I can't find anything about this except for [similarly confused people on forums](https://www.avsforum.com/forum/90-receivers-amps-processors/1456710-official-pioneer-sc-1222-k-owners-thread-4.html). I read the manual, looked in source code search engines, I've done everything I could think of. I feel like I'm trapped in a Buñuel film.

Maybe everything I find after this will have a PRESENTATION PAGE. Maybe I'll wake up tomorrow and the New York Times headline will be PRESENTATION PAGE and I'll end up getting PRESENTATION PAGE on my tombstone. See you tomorrow.
