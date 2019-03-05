+++
title = "Shodan Stories Day 60: The Private Prison Industrial Complex in Houston, Encartele Phones, Bonkers Advertisements, Inmate Surveillance, and Predatory Business Models"
date = 2019-03-04T17:20:55-05:00
draft = false
tags = []
categories = ["100 days"]
+++


I saw a search for "prison phones" and gosh if that isn't a lure I don't know what is. The search was just for "encartele", and doing some Googling I found that [Encartele](https://www.encartele.net/) is a major player in the United States inmate phone service industry. I think this ad will explain what that means:
{{< vimeo 150729069 >}}

## An Encartele Prison Phone on 66.112.68.130
So Encartele charges inmates and their families artificially high phone rates and give paybacks to the wardens running the prisons. The rate differs from prison to prison because _wardens set the rate_ but according to [an ACLU report I read](https://www.aclunebraska.org/en/publications/profiting-lifelines-nebraska-county-jail-phone-systems-lead-high-costs-and-unfair), Encartele rates tend to vary from $7-$10 per 15 minutes. That's a lot. I ended up picking a phone in Houston, since I had previously heard that Houston has [one of the largest prisoner populations in America](https://thecrimereport.org/2018/07/23/how-much-can-houston-cut-its-jail-population/).

The phone was running ssh, telnet, a webserver on 80, and a [VoIP](https://en.wikipedia.org/wiki/Voice_over_IP) on 5060. Everything was totally locked down with authentication - which is good, because otherwise anyone could listen in to inmates' phone calls.

But isn't it a little odd that a phone is running a webserver? Turns out that is how the prison administration listens in to inmates' phone calls. Rather than explain to you how it works, you can watch this informational video Encartele provides.
{{< vimeo 204021146 >}}
This is just awful. How did America get in this situation, where private companies can shake down inmates and pay state employees for the privilege? What's gone wrong with our cultural narratives around crime?

Encartele itself has a very partial answer to this question in a blog post from a few months ago called ["Why Inmate Phones are Not a Public Utility"](https://www.encartele.net/2018/09/why-inmate-phones-are-not-a-public-utility/).
![](/images/100Days/Day60/blog.png)
Apparently regulatory oversight of the inmate phone industry has been politically difficult to institute because of the highly specific nature of inmate phone infrastructure. Their motivations in writing this blog post is very nakedly to convince readers that more federal regulation of Encartele is not the answer.

>Politicians and the ACLU are right about the per-minute costs of inmate calling being too high. Unfortunately, they’re wrong about the best way to lower them.

My guess is it's also to convince their customers - prison wardens - that they are sensible, right headed anti-regulationists, just like any red blooded American should be. I started trying to go down two avenues, read more Encartele promotional documents and read the actual FCC regulations on the industry such as they are, but I started feeling so fatigued. It's godawful and it's only a tiny tiny part of a terrible incarceration system. See you tomorrow.
