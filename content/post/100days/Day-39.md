+++
title = "Shodan Stories Day 39: More TV Torrenting in Toronto, Reckless API Key Exposure, Sonarr, Radarr, Jackett, Ombi, and Deluge"
date = 2019-02-11T20:29:49-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Saw a search just for "gmail.com", I assume to look for anyone who put their email address into their service. I decided to take a look.

## A Torrenting Operation on 162.157.129.215
I like this search because it's device and service agnostic. I ended up just picking the first result and running with it, this one in Toronto. It turned out that the email address that brought me there belonged to the developer of a bittorent client named [Deluge](https://en.wikipedia.org/wiki/Deluge_(software)). I like the pun. The service is running on port 8083.
![](/images/100Days/Day39/deluge.png)
If you can't tell from that screen it had a login. I saw on Shodan that it had some other services running so I decided to give it an `nmap`.

```
👻🌵🔮 $ nmap -p 8075-8500 162.157.129.215 -Pn
Starting Nmap 7.70 ( https://nmap.org ) at 2019-02-11 21:35 EST
Nmap scan report for d162-157-129-215.abhsia.telus.net (162.157.129.215)
Host is up (0.28s latency).
Not shown: 419 filtered ports
PORT     STATE  SERVICE
8081/tcp open   blackice-icecap
8082/tcp open   blackice-alerts
8083/tcp open   us-srv
8084/tcp closed unknown
8086/tcp open   d-s-n
8087/tcp closed simplifymedia
8443/tcp closed https-alt

Nmap done: 1 IP address (1 host up) scanned in 83.16 seconds
```
On 8081 there is a service running called [Sonarr](https://sonarr.tv/) which seems a lot like the torrent management system for tv shows that I found on Day 36.
![](/images/100Days/Day39/sonarr.png)
Sonarr seems to snatch torrents for TV shows from public torrent trackers and then pass those over to a download client (which for this person would be Deluge). You can even get RSS updates when your new episodes have downloaded. In your face Netflix!

On 8082 there's something called [Radarr](https://radarr.video/).
![](/images/100Days/Day39/radarr.png)
Radarr is exactly like Sonarr except for movies. Interestingly I found that these two services were running off of the same device which only had 20GB available of total space. Seemed kind of weird but then I realized that these two services are probably running on a Raspberry Pi and that Deluge is likely running on a networked attached storage device with much more space.
![](/images/100Days/Day39/radarr3.png)
Their API keys for both of these services were exposed, I wasn't sure exactly what I'd be able to do with them but probably nothing good from the perspective of whoever is running this operation.

Nothing showed up in my `nmap` results for port 8085 but I decided to take a look at it in a browser just in case.
![](/images/100Days/Day39/ombi2.png)
I found that it was running a service called [Ombi](https://ombi.io/) which is a kind of media server service much like Plex (which you may remember from way back on day 9) lets you stream your own media content from anywhere with a secure login. Ombi then likely would be running on the NAS device.

That just leaves us with 8086, running a service called [Jackett](https://github.com/Jackett/Jackett) (what's with all the duplicated ending consonants?).
![](/images/100Days/Day39/jackett.png)
Jackett seems like more of a general-purpose torrent to download manager. I found that they were using it just for snatching torrent files from a private torrent tracker called [IPTorrents](https://iptorrents.com/login.php), and they were primarily using it for anime. Heck yeah. Looks like they had just downloaded a show called "[That Time I got Reincarnated as a Slime](https://en.wikipedia.org/wiki/That_Time_I_Got_Reincarnated_as_a_Slime)"
![](/images/100Days/Day39/slime.png)
I ended up watching the first episode. It's about a laid back man who is killed by a mass murderer and then is reincarnated as a slime creature in a fantasy videogame-esque world. It wasn't really my thing, but had reasonably well crafted overarching narratives of finding sanctuary in fantasy in reaction to trauma, the arbitrariness of tragedy, and of persevering while dealing with pain and loss. Another character watches her mother die during the Tokyo firebombing and is about to die herself when she's yanked out of reality by someone summoning her into the videogame world by accident (they wanted a fire demon or something). It's a little hokey though, and some of the emotional notes seem forced and overdone.

![](/images/100Days/Day39/slime2.png)

Whatta face! At least the slime is very cute. See you tomorrow.
