+++
title = "100 Days of Shodan Stories Day 3"
date = 2019-01-06T16:59:25-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Since I didn't do Minecraft servers yesterday I decided to do them today. First I read a [little guide on how to set up a Minecraft server to get a sense of what they looked like](https://minecraft.gamepedia.com/Tutorials/Setting_up_a_server).

### Les Chevaliers Royale Minecraft Server on 97.94.56.211
![](/images/100Days/Day3/LCR2.png)
I actually don't know much about Minecraft, I've never played it. I know it's popular with a wide range of people, and that really dedicated players like to set up servers for group play, so I thought it might be interesting to look around for a server and figure out if I could find the people who were using it. Reading a Shodan blog about them I found that Minecraft servers typically work off of port 25565 so I did a search for IPs running that port, and then I picked the first result.
![](/images/100Days/Day3/Warning.png)
It looked like the server only had 25565 open, so the people who set this up heeded the above advice. From poking around I couldn't tell if they were running this server on their home machine and the and port forwarding through a router or if they had set up a dedicated server. Since the IP is from [Charter/Spectrum](https://www.spectrum.com/), and is set up in St Cloud, Minnesota - not really a hotbed of data centers (although apparently the [worst city in Minnesota to live in](https://www.sctimes.com/story/news/local/2018/10/05/fact-check-st-cloud-worst-city-minnesota-usatoday-census-livability/1536172002/)) - I believe it's probably the former. However I was able to find quite a bit more about this server from a bit of information in the Shodan header.
```
Minecraft Server

Players: 0 online - 20 maximum
Version: 1.12.2 (protocol 340)
Description: Les Chevaliers Royale
```
Googling "Les Chevaliers Royale" yields [a lot of results](https://en.wikipedia.org/wiki/Order_of_Saint_Louis) but well one set of results really stood out as the likely originators of this server, a Christian gaming collective named Les Chevaliers Royale. So I found their [Discord](https://discordapp.com/) chatroom and joined.
![](/images/100Days/Day3/Welcome.png)
They have about 150 members and some hierarchical structure with names based on French military rank. After emoji waving to them a bunch I quickly went looking around to see if I could find them talking about this Minecraft server.
![](/images/100Days/Day3/ServerConfirm.png)
Aha there it is!!! The real gold stuff, people talking about their IP address out in the wild. It's a great feeling to make this kind of contact, like putting the final puzzle piece into a jigsaw puzzle.
![](/images/100Days/Day3/Pray1.png)
I stuck around and lurked at their conversations a bit to see if I could find out anything more about them. They were talking about homework and things like that and they seemed to be teenagers, and most of their conversations had too high of a barrier for me, with memes, in jokes, and cultural references that I didn't understand. And some of their discussions were repulsive to me, they seem to be homophobic with an extra edge of religious justification.
![](/images/100Days/Day3/Meme.png)
But some of their conversations, especially 3AM ones, had the same kind of meandering yet emotionally lucid cadence that I remember from AIM chatrooms that I was in as a teen. I remember always being more comfortable late at night in a chatroom because I knew fewer people would be on and I could have a 1 on 1 conversation. Maybe because they are all Christian they tend to speak with a higher level of pathos and candor than I would have expected a group of internet gamer friends to share. They discuss chronic pain, have a channel for prayer requests for the problems in their and their friends's lives, discuss their faith and troubles with belief, have earnest discussions about American racism.
![](/images/100Days/Day3/Meander2.png)


See you tomorrow.
