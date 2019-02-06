+++
title = "Shodan Stories Day 32: Propaganda in Pyongyang"
date = 2019-02-05T20:55:59-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I saw someone had compiled a list of every Shodan-discovered server running in North Korea. To be honest I was a little surprised that there would be much outward-facing internet in North Korea, so I decided to take a look.

## Media Ryugyong on 175.45.176.80
Most of the servers seemed to be mail servers, but some of them were running webpages. I picked the first one I found that was running a web page.
![](/images/100Days/Day32/media.png)
The website is clearly meant for an international audience as it comes not only in Korean but also with translations to Russian, English, Chinese, French, and Spanish. After looking around I figured out that the purpose of this site is to collect patriotic pictures and videos of various aspects of North Korean life.
![](/images/100Days/Day32/supremeleader2.png)
There are many many many photo albums of Kim Jong Un.
![](/images/100Days/Day32/kimandxi.png)
Here's a picture of Kim Jung Un meeting with Xi Jinping I remember seeing on the South Korean TV station a bunch of times way back on day 24! I wonder if they got it from here? Or maybe all of these political meeting photos all kind of look the same.

The website also has about 100 videos that vary in content from "check out this cool mountain" to "we the Korean people are soul bound to follow the Party down the only road into the future".
![](/images/100Days/Day32/mediaA.png)
Quite a few of the videos are extremely long (15+ minutes) patriotic songs. Again I could tell that these videos were clearly meant for an international audience, as they had english subtitles and frequent asides to give context.
![](/images/100Days/Day32/mediaB.png)
Some of the tourist-focused videos were really interesting. I found myself watching them for almost two hours.
![](/images/100Days/Day32/videostills.png)
There are videos about beaches, patriotic dogs, military factories, military airplanes, a [US navy boat that the North Koreans captured from the United States in 1968 that has since been turned into a museum](https://en.wikipedia.org/wiki/USS_Pueblo_(AGER-2)), memorials of The War, the 38th parallel, US imperialism, fish pickling factories, special babies, a water park, and more. Many of them take the form of song.
![](/images/100Days/Day32/uncloak.png)
It's kitschy for sure, but I find it greatly unsettling.

The web page is called "Media Ryugyong" but when trying to search for it I at first only found information about a North Korean hotel named Ryugyong, that's [apparently been under construction since 1987 and has the Guinnes world record for largest uninhabited building](https://en.wikipedia.org/wiki/Ryugyong_Hotel). After looking a little harder I found that it's listed as one of [only a handful of publicly accessible North Korean webpages](https://nkinternet.wordpress.com/websites/), but with very little English-language information available beyond that. I did find that it was made by a company called [Ryugyong Computer](https://www.northkoreatech.org/2018/10/10/north-korea-launches-an-internet-portal/), but then I couldn't find any information about that company.

I was a little curious about how exactly I'm connecting to this website. Physical cables lead from my home all the way there, and I read that the only link to the internet outside of North Korea is [a cable between Pyongyang and Dandong in China](https://en.wikipedia.org/wiki/Telecommunications_in_North_Korea#International_Internet_access). I checked traceroute to see if I could get a complete picture of the trip.
```
➜  sandbox traceroute 175.45.176.80
traceroute to 175.45.176.80 (175.45.176.80), 64 hops max, 52 byte packets
 1  192.168.0.1 (192.168.0.1)  10.712 ms  5.223 ms  3.130 ms
 2  * * *
 3  be61.nycynymy02h.nyc.rr.com (68.173.202.74)  19.082 ms  23.958 ms  19.198 ms
 4  agg113.nyquny9101r.nyc.rr.com (68.173.198.42)  11.413 ms  37.942 ms  44.836 ms
 5  bu-ether15.nycmny837aw-bcr00.tbone.rr.com (66.109.6.76)  18.098 ms
    bu-ether25.nycmny837aw-bcr00.tbone.rr.com (107.14.19.22)  25.559 ms  21.052 ms
 6  0.ae1.pr0.nyc20.tbone.rr.com (66.109.6.163)  27.620 ms
    0.ae2.pr0.nyc20.tbone.rr.com (107.14.19.147)  29.842 ms
    0.ae0.pr0.nyc20.tbone.rr.com (66.109.6.157)  24.038 ms
 7  ix-ae-10-0.tcore1.n75-new-york.as6453.net (66.110.96.13)  26.842 ms  16.637 ms
    ix-ae-6-0.tcore1.n75-new-york.as6453.net (66.110.96.53)  18.283 ms
 8  if-ae-9-2.tcore1.nto-new-york.as6453.net (63.243.128.121)  83.721 ms  84.435 ms  81.125 ms
 9  if-ae-12-2.tcore1.sqn-san-jose.as6453.net (63.243.128.29)  89.536 ms
    if-ae-0-2.tcore1.sqn-san-jose.as6453.net (63.243.128.31)  82.377 ms
    if-ae-12-2.tcore1.sqn-san-jose.as6453.net (63.243.128.29)  80.993 ms
10  63.243.205.90 (63.243.205.90)  84.526 ms
    63.243.205.46 (63.243.205.46)  85.008 ms  92.695 ms
11  219.158.117.1 (219.158.117.1)  264.207 ms  245.906 ms  248.608 ms
12  219.158.115.122 (219.158.115.122)  279.363 ms  321.038 ms  280.110 ms
13  219.158.102.214 (219.158.102.214)  276.315 ms  281.610 ms  277.184 ms
14  * * *
15  * * *
16  * * 219.158.39.42 (219.158.39.42)  284.168 ms !X
17  * * *
18  * * *
19  219.158.39.42 (219.158.39.42)  288.479 ms !X * *
20  * * *
21  * * *
22  * * 219.158.39.42 (219.158.39.42)  407.138 ms !X
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  * * *
29  * * *
30  * * *
31  * * *
32  * 219.158.39.42 (219.158.39.42)  284.029 ms !X *
33  * * *
34  * * *
35  * * *
36  * * *
37  219.158.39.42 (219.158.39.42)  416.278 ms !X * *
38  * * *
39  * * *
40  * * *
41  * * *
42  * * *
43  * * *
44  * * *
45  * * *
46  * * *
47  * * *
48  * * *
49  * * *
50  * * *
51  * * *
52  * * *
53  * * *
54  * 219.158.39.42 (219.158.39.42)  310.160 ms !X *
55  * * *
56  * * *
57  * * *
58  * * *
59  * * 219.158.39.42 (219.158.39.42)  277.531 ms !X
60  * * *
61  * * *
62  * * *
63  * * *
64  * * *
```
Clearly I couldn't, but 219.158.39.42 at least seems to be in China. At least that's something. See you tomorrow.
