+++
title = "Shodan Stories Day 52: The Littleborough Losers in Ramsgate, Having a Few Pints with the Lads, Fantasy Football Since 1995, Rick's Footy Challenge, and Wayne Rooney the True Ledge"
date = 2019-02-24T23:48:26-08:00
draft = false
tags = []
categories = ["100 days"]
+++

I saw an amazing search on Shodan today, it was just named "self-explanatory" and the search was just for the word "losers". How could I say no?

## Littleborough Losers on 94.7.201.171
The results were pretty varied, there's apparently a sex kink that has to do with being dominated and called a loser and so quite a few results were communities related to that, but I found a result in England that more closely fits my particular kink: 90s web design.
![](/images/100Days/Day52/firstlook.png)
"Fulfill your Fantasy!" Beautifully, amazingly, tantalizingly it's the website for a group of friends' fantasy football league (in this case what we over here call soccer) from all the way back in _2005_. Try finding anything remotely like this on Google! No search engine optimization here! Yes that's a color burned picture of [Wayne Rooney](https://en.wikipedia.org/wiki/Wayne_Rooney) as the background, and yes it's tiled. Yes the soccer ball is a spinning gif. There's a bit of code in the page - the kind of javascript that simply doesn't work anymore - that indicates that this group had been going since 1995.
```
msg_a = "Welcome to Littleborough Losers Fantasy Football League - it's not a race but a marathon!";
msg_b = "";
msg_c = "";
msg_d = "";
msg_e = "Formed in 1995 - who will be champion in this - the 11th season?";
msg_f = ""
```

How could a little website like this survive for so long?
![](/images/100Days/Day52/certificate.png)
I got a clue from the HTTPS certificate that it's running on a Synology Network Attached Storage device, the kind we've now seen several times on our little journey together. It's also got a Synology login on port 5001.
![](/images/100Days/Day52/synology.png)
My assumption is that matthew882, for reasons of nostalgia or simple perversity, decided to migrate their old website from a dedicated webhost to the network attached storage they had recently gotten from his home.  

Many of the links no longer work, but luckily we are able to get a glimpse at the trophy.
![](/images/100Days/Day52/trophy.png)
Truly an honor worth fighting for. The hall of fame is also still working, and seemingly still active.
![](/images/100Days/Day52/hall.png)
Puzzlingly it's been updated through 2018, meaning that these friends must still be playing and updating this part of the site at least, if not any others. One wonders if they pass the trophy each time or get a new one each year. Results go back to 1995, and you see a lot of the same names repeating over over the two decades of this friend group. Because of this list I was able to find out who matthew882 is, but let's leave him alone, we have more interesting things to pursue.

One of the links on the main page, the one for the transfer password, is to a now long gone Geocities site called [Ricks Footy Challenge](http://www.geocities.com/ricksfootychallenge/password.htm). Sometimes what's been lost can still be found, and yes, I was able to find this page on the [Internet Archive](https://web.archive.org/web/20040929004518/http://www.geocities.com/ricksfootychallenge/index.html)
![](/images/100Days/Day52/rickspassword.png)
I know I know, you're excited too. Yes it's Comic Sans on the web. Apparently this page had gotten so popular at the time that it was overwhelming the Geocities bandwidth: as you can see from that message Rick (I assume), had set up a backup page for the password.

But what is this password of the week for? Maybe Ricks Footy Challenge Home would have answers?
![](/images/100Days/Day52/footychallenge.png)
It did not in and of itself, but it is an incredible page. The font color/background contrast makes it barely legible. aThat's a scrolling marquee of football news that I can only assume Rick updated by hand each week.

There were some links on the page as well that gave me some clues. It seemed like maybe it had to do with the [Daily Telegraph's](https://en.wikipedia.org/wiki/Telegraph_Media_Group) sports pages and fantasy football forum, so I took a look again with the [Internet Archive](https://web.archive.org/web/20050917223011/http://www.fantasygames.telegraph.co.uk/portal/main.jhtml?grid=P9&view=GAMES) to see if I could get any clues.  
![](/images/100Days/Day52/telegraph.png)
I didn't immediately find any places for inputting a "transfer password", and it was a long time before I came across this full explanation.
![](/images/100Days/Day52/fiso.png)
While the exact mechanics of where and how you use the password for still elude me, we now know that the Daily Telegraph Fantasy Fottball transfer password is added to the Telegraph Fantasy Football Forum every week, and that it's necessary in order to make a transfer, which I believe is a trade of players. Why a password would be necessary for this is still unknown.

See you tomorrow.
