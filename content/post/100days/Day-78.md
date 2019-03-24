+++
title = "Shodan Stories Day 78: The Ol' Unix Nostalgia in the Netherlands, Fortune | Cowsay, and the Mysteries of Tranquility Quidor"
date = 2019-03-23T12:52:22-04:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I've been trying to write a paper about the waste industry and garbage, so I decided to search on Shodan just for the word "garbage" and see what I get.

## Telnet Service on 62.133.200.27
There were about 100 results, most of them garbage themselves. But I found one in the Netherlands that perplexed me. It showed up in my Shodan search because Shodan had gotten the following response on port 7777:
```
remote: 46.178.111.82 48586
local: 62.133.200.27 7777
0
 1:43PM  up 2023 days,  3:20, 0 users, load averages: 1.14, 1.13, 1.16

What I've done, of course, is total garbage.
		-- R. Willard, Pure Math 430a
```
I had a hunch at what I was seeing here, but I wanted to test it out first myself.
```
👻🌵🔮 $ nc 62.133.200.27 7777
remote: [REDACTED ;)] 55065
local: 62.133.200.27 7777
0
 3:44AM  up 2028 days, 17:21, 0 users, load averages: 0.30, 0.37, 0.41

It would be nice if the Food and Drug Administration stopped issuing
warnings about toxic substances and just gave me the names of one or
two things still safe to eat.
                -- Robert Fuoss
```
This looks like the output from the old unix command, [fortune](https://en.wikipedia.org/wiki/Fortune_(Unix)). Back when I was learning bash one of the first things I learned how to do was pipe `fortune` to `cowsay`. `fortune` outputs various quotes and sayings that are full of the kind of asinine nerd humor that kept gen x unix programmers smirking while their code compiled. I kept netcatting the port and kept getting different sayings and quotes, all of which seemed like they were from `fortune`. I found that it was also running on port 23.
```
👻🌵🔮 $ nc 62.133.200.27 23
remote: [REDACTED ;)] 64347
local: 62.133.200.27 23
0
 4:21AM  up 2028 days, 13:59, 0 users, load averages: 0.46, 0.46, 0.40

Fudd's First Law of Opposition:
        Push something hard enough and it will fall over.
```
It's definitely fortune. If that's not enough to convince you, I ran it so many times that I eventually got an error
```
👻🌵🔮 $ nc 62.133.200.27 23
remote: [REDACTED ;)] 63466
local: 62.133.200.27 23
0
 4:48AM  up 2028 days, 18:25, 0 users, load averages: 0.57, 0.47, 0.39

Usage: fortune -P [] -a [xsz] [Q: [file]] [rKe9] -v6[+] dataspec ... inputdir
```
Don't worry it still works, I don't know exactly what went wrong that time. You can see from the return that it has been up for 2028 days, which is over five years.

Who has been running two fortune telnet services for five years, and why?

On port 13 it looks like they are also running a date/time service.
```
👻🌵🔮 $ nc 62.133.200.27 13
Sun Mar 24 05:04:15 2019
```

I ended up finding a bunch about this person, but I figured I should leave them alone. If you ever want to find them, you may find the phrase "tranquility quidor" to be helpful.

See you tomorrow.
