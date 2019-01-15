+++
title = "Shodan Stories Day 11: Machine Learning in Beijing and the Mysteries of 126 and 163"
date = 2019-01-14T14:27:56-05:00
draft = false
tags = []
categories = ["100 days"]
+++
Today I went looking for [MongoDB](https://www.mongodb.com/) databases. I used MongoDB back in Shawn Van Every's servers class, I remember feeling pretty cool using a [NoSQL database](https://en.wikipedia.org/wiki/NoSQL). Shodan indicated that MongoDB tends to work off of port 27017 so that's where I started looking.

## The Shell of Someone's Machine Learning Blog on 35.185.145.24
I picked one of the first results I found on Shodan. According to Shodan it's located in Singapore and hosted on Google Cloud services. After running `nmap` on the IP I saw it had port 80, the http port, open so I decided to visit it in a browser.
```
➜  sandbox git:(master) ✗ nmap -p- 35.185.145.24
Starting Nmap 7.70 ( https://nmap.org ) at 2019-01-14 18:02 EST
Nmap scan report for 24.145.185.35.bc.googleusercontent.com (35.185.145.24)
Host is up (0.21s latency).
Not shown: 65528 closed ports
PORT      STATE SERVICE
22/tcp    open  ssh
80/tcp    open  http
3010/tcp  open  gw
8080/tcp  open  http-proxy
8088/tcp  open  radan-http
8989/tcp  open  sunwebadmins
27017/tcp open  mongod

Nmap done: 1 IP address (1 host up) scanned in 1507.34 seconds
```
![](/images/100Days/Day11/ailab.png)
It looks like a blog named AI Lab with a bunch of posts about how to use quite an extensive range of machine learning tools. Additionally it has posts about songs and music. Some things are off though. None of the media embeddings work (i.e. none of the songs play), every post has 666 likes and no comments, some of the code formatting is broken and unreadable in the posts, and quite a few of the image links are broken. Also it has no DNS entry, it's only resolving to the googleusercontent.com URL. Clearly this blog is not meant for public eyes. The bottom has a note about the author: their name is Leo, and you can message them on WeChat.
![](/images/100Days/Day11/wechat.png)
So now I really wanted to know about the history of this blog and I got kind of overly obsessed with why it's in this quasi state of reality. I thought about messaging Leo, but I thought that would be too weird right off the bat, though I did check Leo's WeChat page and it said that they were in Beijing, not Singapore. That makes sense for two reasons: the website is in simplified Chinese, and not traditional like they use in Singapore, and Google doesn't have facilities in China to my knowledge so if you want to use Google hosting and you're in Beijing then Singapore seems like a close option.

There's a signup and login (?) at the top right I thought about trying to join but decided that that would be too weird also. I tried probing all the other open ports and one of them yielded returns, 8080, which seems to be hosting an entirely different, though related, website.
![](/images/100Days/Day11/wiki.png)
This is kind of like a documentation website that goes through many specific tools than in the blog, which does more deep dives on things like processes and methodologies.
Now I noticed that there's the friendly Github Octocat logo in the corner (which even waves when you hover over it), which I was hoping would be Leo's Github page. It was not a link to Leo's Github page. Instead it's a link to git.riverrun.cn.
![](/images/100Days/Day11/riverrun.png)
This is a [Gogs-based](https://gogs.io/docs) self hosted Git service, so it's essentially someone's private version of Github. riverrun.cn itself does not appear to exist as a website, and instead prompts a download of a blank file whenever it is visted in a browser, but it does have a WhoIS entry.

```
Domain Name: riverrun.cn
ROID: 20140703s10001s71703193-cn
Domain Status: ok
Registrant ID: 6681981404378845
Registrant: 侯光敏
Registrant Contact Email: guangmin001@163.com
Sponsoring Registrar: 成都飞数科技有限公司
Name Server: f1g1ns1.dnspod.net
Name Server: f1g1ns2.dnspod.net
Registration Time: 2014-07-03 17:14:08
Expiration Time: 2019-07-03 17:14:08
DNSSEC: unsigned
```
163.com, I'd seen that before! As embedded javascript on the first web page.
![](/images/100Days/Day11/163.png)

Now at this point I did two deep dives. One to find out more about those 126 and 163 urls, and the next to find out more about Leo and guangmin001@163.com.

The first might be the most interesting, and the [Quora question I'm linking to has a pretty decent answer](https://www.quora.com/What-does-126-and-163-mean-in-Chinese-language). 163 and 126 were commonly used numbers back in China's dialup era to connect to the web. The numbers still connote "internet service" to people even though dialup is no longer used, and 163.com is one of the most commonly used email service provider (much like gmail for many Americans), owned by a company called [NetEase](https://en.wikipedia.org/wiki/NetEase). NetEase seems a little bit more like Verizon than Google though, the company has a wide reaching scope and a successful email hosting operation but doesn't seem to be on the forefront of innovation and growth. Their main domain property, [www.163.com](https://www.163.com/), even looks a little bit like yahoo.com. They do have a successful music streaming service, and that's where those nonfunctioning music embeds in Leo's website were pointing toward.'

The second got a little too doxxy for me to want to write about too much. But I found that Leo seemingly has a penchant for raw IPs over domain names, and Guangmin, in addition to running the Riverrun Network, created a protocol for streaming television which is now used by a service called [Feng Mi](https://www.fengmi.tv/).

But what was the MondoDB database being used for in the first place? My guess is probably to manage accounts on that login thing I ignored. But why make an account on someone's hidden and half-finished blog? See you tomorrow.
