+++
title = "Shodan Stories Day 37: Minitel"
date = 2019-02-09T21:50:14-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Oh Minitel. I never expected to find you, here on the very World Wide Web that killed you.

## 3614 TEASER emulator on 62.210.93.204
I saw a recent search on Shodan for "ttyd terminal shell".  [ttyd](https://github.com/tsl0922/ttyd) is a service for sharing your Terminal over the web, meaning that an insecure ttyd server would mean total access over someone's computer (assuming they were porting root). I decided to take a look. Of the 12 results most were just named 'ttyd - terminal' and most of those were inactive, but one stood out. One... was different.
![](/images/100Days/Day37/firstlook2.png)
The name of this web server, running on port 8080, is "Serveur Minitel 3614 TEASER". Deep in my brain something stirred, an anchor was let loose, but couldn't immediately pull the memory up.
![](/images/100Days/Day37/teasermodems.png)
Minitel...
![](/images/100Days/Day37/bomb.png)
Minitel! The web before the Web! Minitel! The France Wide Web! The little telephone line modems with the black and white terminals. The tiny boxes, the closed systems, the terrible,  beautiful graphics.

Minitel was a network all over France, beginning in the late 70s and lasting all the way until 2012. It ran over the phone line, allowed you to graphically connect to different services where you could join a chatroom, pay a bill, check the weather, message your friend, etc. All in the 80s, long before websites existed. Before HTTP existed. It was the technical marvel of the world. In the 80s, France really was the height of modernity. Everyone else just had fax machines. It was a hugely expensive piece of infrastructure, a vast government project. All citizens got a free Minitel terminal. Imagine a government giving out free laptop computers to all of its citizens.

This was clearly an emulated Minitel terminal connected to a service called 3614 TEASER. The graphics, the AZERTY keyboard, the fact that Minitel was in the webpage's title. There were some instructions on the left side of the emulation but they only explained how to type into the emulator. Why did this exist? Who made it? What was going on?

I decided to check with `host` to see if this was a named website. I found also that the page was running javascript from a source called 3614teaser.fr, so I checked that too.
```
➜  ~ host 62.210.93.204
204.93.210.62.in-addr.arpa domain name pointer mail.michot.fr.
➜  ~ host michot.fr
michot.fr has address 62.210.93.204
michot.fr mail is handled by 10 nospam.spamfree.fr.
michot.fr mail is handled by 200 nospam2.spamfree.fr.
michot.fr mail is handled by 100 nospam1.spamfree.fr.s
➜  ~ host 3614teaser.fr
3614teaser.fr has address 62.210.93.204
```
Interestingly the IP has the domain name of mail.michot.fr, michot.fr, and 3614teaser.fr. That's some heavy lifting. I visit michot.fr in my browser. It's not very exciting.
![](/images/100Days/Day37/michot.png)
That's the same thing that is running on port 80 of the IP so confirmed that indeed it is that url. mail.michot.fr is the same thing. 3614teaser.fr is different.
![](/images/100Days/Day37/teaser.fr.png)
It's a website dedicated to the history of the 3614 TEASER service. There are some links to PDFs of articles from the 90s, a picture of a real Minitel terminal running the service, a link to the emulator I had originally discovered, and a few other links to related Minitel things. Clearly this website was made as a shrine to 3614 TEASER, and the emulation of the service was a passion project. But what was 3614 TEASER. I can't read any of the articles as they are in French and the burden of getting machine translation of a PDF is just a little too high for me. The same holds true of the emulation itself, as it's not copy/pasteable so I can't put it into Google translate.
![](/images/100Days/Day37/lost.png)
Which means I'll have to figure out what TEASER was the old fashioned way. By Googling it.
![](/images/100Days/Day37/minitelorg.png)

There are surprisingly few results - and none in English. Among the first there is a website dedicated to documenting the history of the Minitel as much as possible, [minitel.org](https://minitel.org/), which mentions 3614 TEASER only in reference to the very site I was just on, as part of a list of extant emulated Minitel services.
![](/images/100Days/Day37/services.png)
I ended up going to French Wikipedia and finding the page for one of the founders of France-Teaser, a man named [Jean-René Vidaud](https://fr.wikipedia.org/wiki/Jean-Ren%C3%A9_Vidaud).
![](/images/100Days/Day37/jeanclaude.png)
France-Teaser created and ran 3614 Teaser and it was the first service that connected the internet to Minitel. You could use it to check your email, read the news, and possibly other things. But look at that image a little longer. Vidaud is with his cofounder Jean-Claude _Michot_. If you remember, michot.fr is the domain name of this whole operation. Thus, in all likelihood, Jean-Claude Michot made this web shrine for the Minitel service he made 25 years ago.

Jean-Claude, what do you think of when you think of Minitel? A broken dream? The best years of your life? Clearly, you're still thinking about it. But there are other people out there still thinking about it too.

![](/images/100Days/Day37/community.png)
See you tomorrow.

<br>

<br>

<br>
PS

An interesting side story: the webhost for this emulator is Iliad, one of France's biggest telecoms. Iliad was founded and is still owned by the multibillionaire Xavier Niel, who got his start in the industry by creating Minitel services. And not just any Minitel services, but chatrooms and chatlines for cybersex. France really has it figured out.
