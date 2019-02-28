+++
title = "Shodan Stories Day 55: Dancing with Skunks and Annotating Goats in Fremont, Ornamental Hermits, Gopherspace, and the Mysteries of Time"
date = 2019-02-27T13:39:11-05:00
draft = false
tags = []
categories = ["100 days"]
+++


Some Cisco routers say "SAN FRANCISCO" when `telnet`ing into them, and so someone had searched for that on Shodan looking for these routers (they say other things too of course, but that's just an easily searchable commonality). That kind of dragnet obviously pulls in a lot of other stuff too and I was particularly taken with one result.

## An Ornamental Hermit on 74.207.243.202
What caught my eye on this IP was that Shodan was indicating that it was running gopher on port 70. [Gopher](https://en.wikipedia.org/wiki/Gopher_(protocol)), as you may know, was a hypertext transfer protocol that existed alongside HTTP in the early 1990s, and had a brief period of popularity peaking around 1993 before becoming overwhelmed by the World Wide Web. Gopher is primarily text based and would return hierarchically structured text documents with links and [didn't have the kind of hypermedia support that web sites have](https://motherboard.vice.com/en_us/article/9kwek8/long-live-gopher-the-techies-keeping-the-text-driven-internet-alive). Last I heard a few years ago there were supposedly only a few hundred pages in "gopherspace" meaning that this was a pretty rare find, so I installed a [gopher plugin on Firefox](https://addons.mozilla.org/en-US/firefox/addon/overbitewx/), put on Aphex Twin to get me in the 1992 mood, and got to exploring.

The first thing I noticed was that the gopher page, which was named __gopher.stjo.hn__ seemed to be completely different from the one running on the regular port 80 webserver, __annotatedtmg.org__.

![](/images/100Days/Day55/gopher.png)
__gopher.stjo.hn__

![](/images/100Days/Day55/mountaingoats.png)
__annotatedtmg.org__

Before long I was able to determine that port 80 was also running another webserver, this one actually a mirror of the gopher page.
![](/images/100Days/Day55/stjohn.png)
__www.stjo.hn__
I'm guessing the font choice is as a way to encourage people to try gopher. But anyway: this is pretty surprising. It's entirely possible to have multiple domain names hosted on a single IP address, but it's pretty weird to see a situation where they have seemingly belong to entirely different people. Meanwhile the IP itself has a domain name pointer of... none of this addresses.

```
👻🌵🔮 $ host 74.207.243.202
202.243.207.74.in-addr.arpa domain name pointer fuzzjunket.com.
```

It instead is registered to __fuzzjunket.com__. Luckily that just redirects __to www.stjo.hn.com__ and there isn't too much mystery there to solve. Just checking the others to see for clues.

```
👻🌵🔮 $ host annotatedtmg.org
annotatedtmg.org has address 74.207.243.202
annotatedtmg.org mail is handled by 50 fb.mail.gandi.net.
annotatedtmg.org mail is handled by 10 spool.mail.gandi.net.
👻🌵🔮 $ host www.stjo.hn                                        
www.stjo.hn has address 74.207.243.202
www.stjo.hn has IPv6 address 2600:3c01::f03c:91ff:fe24:69e8
👻🌵🔮 $ host gopher.stjo.hn
gopher.stjo.hn has address 74.207.243.202
👻🌵🔮 $ host fuzzjunket.com
fuzzjunket.com has address 74.207.243.202
fuzzjunket.com has IPv6 address 2600:3c01::f03c:91ff:fe24:69e8
fuzzjunket.com mail is handled by 10 mail.fuzzjunket.com.
```

Verified they are all on the same IP. I checked `whois` and saw that their webhost is [Linode](https://www.linode.com/), which does cloud hosting, so maybe Linode is saving on IP addresses by doubling up. Or maybe these two are friends and decided to save by splitting a virtual machine. Who are these two anyway?

### St John Karp
As you can read from his description, St John Karp is a "writer, historian & ornamental hermit". An ornamental hermit, as we all know, is the [living predecessor to the garden gnome](https://en.wikipedia.org/wiki/Garden_hermit), a man who very wealthy Europeans paid to live in a small hut on the outskirts of their property, dress as a druid, and live a humble rustic life for the observation and amusement of the landowner.
![](/images/100Days/Day55/gardenhermit.png)

I would posit that this man is not in fact an ornamental hermit. But he has written a couple of books and several plays. He seems to be a bit of a [intentionally quirky person](https://www.kirkusreviews.com/author/st-john-karp/), so I think the use of gopher plays into that.

### Annotated Mountain Goats
Another otaku weirdo's website, the Annotated Mountain Goats is dedicated to one man's extreme fandom for the indie rock band [the Mountain Goats](https://en.wikipedia.org/wiki/The_Mountain_Goats). Over the past many years he has attempted to uncover every hidden meaning and reference in every one of this band's songs. It seems as though he himself has gotten a fair bit of attention from the Mountain Goats fandom community, and in his blog posts he thanks many people for sending in emails with tips and ideas. He also makes free band-related buttons and will mail them to anyone who sends him an empty envelope. It's very sweet, and very twee, and reminds me of being a teenager, listening to _The Sunset Tree_, one of the band's albums. I remember having that album on my iPod, sitting in a yellow chair my parents owned, listening to it while working on my AP physics homework.

Because I'm also an obsessive otaku, I've used [last.fm](https://www.last.fm) to collect metadata on all the music I listen to for the past 13 years. I can see that I last listened to the Mountain Goats on October 6th, 2008, a Monday. More than ten years ago. I listened to "You or Your Memory", which, I now know from the Annotated Mountain Goats, is about the main singer looking back on his teenage years.

How's that for a tidy ending? See you tomorrow.
