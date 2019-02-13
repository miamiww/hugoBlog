+++
title = "Shodan Stories Day 40: Blue_7 in Beijing, GGGG, Evading Government Censures, Server Login Lists, Abandoned Blogs, Shadow Socks, Telegram Chat Rooms, and the Mystery of Using URLs as Passwords"
date = 2019-02-12T17:20:20-05:00
draft = false
tags = []
categories = ["100 days"]
+++

I spent so long trying to figure out what I found today that I've forgotten how I found it. I think it was from someone's search for "USB", but I'm now unable to recreate the search.

## A Mystery on 118.24.95.11
However I discovered this IP, I first arrived at what looked like a normal blog on port 8083.
![](/images/100Days/Day40/firstlook.png)
There is a very ~hacker~ image of a guy in ad hoody as the author's picture. However most of the content was empty and it had a lot of default posts with fake engagement. It reminded me of the unfinished blogs I saw on days 11 and 22. This one had a nice interactive HTML5 canvas for a background with some cool shapes. The canvas seemed to make my CPU go into overdrive though so I didn't leave the tab open for very long.

I saw that it was also running services on 80 and 443, classic website behavior. But it wasn't a website, as I found out. 80 wasn't actually hosting anything. 443 was, and had a certificate letting me know that the url for this page is "swpuhelloworld.cn" (now swpu could be Southwest Petroleum University, a Chinese University, but I didn't get anywhere with this line of investigation). But all it had on it was a JSON file, no HTML, no nothing.
![](/images/100Days/Day40/json.png)
If you look carefully you'll see that it's a list of IP addresses, their location, and methods of logging into them. I got kind of freaked out seeing this. Clearly there was something deep going on here. First the guy in the hoodie in the blog and now this!!

Parsing through that JSON I found that there were three URLs being used as passwords: http://gggg.rocks, www.darrenliuwei.com, and www.sphard.com. In addition there were references to addresses for these servers called "ssurl". I would like to now say that it took me hours to discover what ssurl meant. Let's come back to those in a bit, and look first at those URLs.

### Blue_7 on gggg.rocks
gggg.rocks is a Wordpress site with a single blog post.
![](/images/100Days/Day40/gggg.png)
It's a list of IP addresses with ssh login information for all of them and a link to a service that checks whether or not an IP address is blocked in China. Immediately I had a hunch: people are using these servers to get around the Chinese government's firewalls. The only other thing in the post  a link to Blue_7's [Telegram](https://telegram.org/) chatroom.
![](/images/100Days/Day40/telegram.png)
What's Blue_7? The description there on their Telegram page says they are a "tea drinking club". What's Telegram? It's a chat app that requires you install it before you can login to a chatroom, and advertises itself as heavily encrypted with a major emphasis on privacy and security. Messages in Telegram also "self destruct" after a user-defined time limit. My hunch is that Blue_7 is a group that sets up and disseminates information about these servers, like a hacking collective for getting around the government firewall. No I didn't get Telegram and join their group. I wanted to but I had other pressing things to look into.

### www.darrenliuwei.com and www.sphard.com
These two blogs are virtually identical and belong to the same man.
![](/images/100Days/Day40/darren.png)
He makes a lot of tech instructional videos and has several thousand Youtube followers. Based on reading comments on his Youtube videos I think he has duplicate blogs because one of his blog urls got banned in China, maybe because he was participating in this kind of firewall-evading. As what seems to be a total red herring for me he has exactly the same blog theme as the original blog that I found, down to the interactive background canvas that eats up my computer's CPU.
![](/images/100Days/Day40/interactive.png)
I assume now that the original blog I found probably just copied this guy's blog style.


### ssurl
My first hunch was "secure shell url". Wrong. ssurl is not a commonly used acronym and is not truly Googalable, though that didn't stop me from trying.
![](/images/100Days/Day40/shadowsocks.png)
Finally I arrived here, to [Shadowsocks](https://en.wikipedia.org/wiki/Shadowsocks). From Wikipedia: "Shadowsocks is a free and open-source encrypted proxy project, widely used in mainland China to circumvent Internet censorship." Of course! Proxies! Somehow my brain was blocking out the word "proxy" and I had to reconstruct the idea in my own head before I could search for it. As I'm sure you can now guess, ssurl stands for shadowsocks url and is the url created by a proxy server when running shadowsocks and is what it uses for tunneling.

I'm sure you're wondering: how long exactly were you searching on Google? An hour? Two? Well I'm here to say life is a little richer if some of the mysteries are get left unsolved. See you tomorrow.
