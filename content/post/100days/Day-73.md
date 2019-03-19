+++
title = "Shodan Stories Day 73: Automating Application Testing in Tel-Aviv, Jenkins, and Extremely Secure Devops"
date = 2019-03-17T23:06:33-04:00
draft = true
tags = []
categories = ["100 days"]
+++

I recently read about something called [Jenkins](https://jenkins.io/), "the leading open source automation server". The name and the logo reminded me of the now long gone [Ask Jeeves](https://en.wikipedia.org/wiki/Ask.com), a search engine that I used when I was first getting online back in the 90s.

## Jenkins Automation Server on 52.73.234.8
I just searched for "Jenkins" and looked around until I found a result without a login. It was in Ashburn, Virginia which almost certainly meant it was running on AWS in the [giant Amazon server facility there](https://www.datacenters.com/amazon-aws-ashburn).
Checking `host` confirms that it's running on an AWS EC2.
```
👻🌵🔮 $ host 52.73.234.8
8.234.73.52.in-addr.arpa domain name pointer ec2-52-73-234-8.compute-1.amazonaws.com.
```
It was running one thing, a webserver on port 8080.
![](/images/100Days/Day73/firstlook.png)
So Jenkins is for... automating... stuff. I didn't really have the time to understand it fully. But it looks here like they were attempting to test out several different applications for [Samsung Galaxy phones](https://www.samsung.com/us/mobile/galaxy/).
![](/images/100Days/Day73/variables.png)
I couldn't run anything myself but I was able to see a lot of information about these apps.
![](/images/100Days/Day73/yaral.png)
The one named "yuvalisGod" was pretty confusing to me, until I realized that "yuval" was the name of one of the users of this server.
![](/images/100Days/Day73/names.png)
Given all of this I was able to figure out pretty definitively that this server belonged to the Tel Aviv office of a company named [Perfecto Mobile](https://www.perfecto.io/).

They had various API keys exposed and if I were a black hat I'd probably be able to do a lot of damage. Shows the importance of having infosec as part of your devops. See you tomorrow.
