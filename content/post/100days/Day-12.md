+++
title = "Shodan Stories Day 12: Influencer to Brand Marketplace and Authentic Content Platform in San Jose, Damaging My Klout Score via Unauthorized API Calls, GraphQL IDEs, and the Center of the Internet"
date = 2019-01-15T20:20:27-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Today I saw a top search for something called "GraphQL". Taking the bait on the unknown, I started looking.

## A Startup Named Zipline's API Testing Staging Space on 184.169.231.191
The first thing I noticed about GraphQL's distribution on Shodan was that it was all in the US. The second was that it was, by a huge margin, all in Ashburn, Virginia. After doing a quick google search I figured out that this is certainly because [Amazon has so many datacenters there](https://www.washingtonpost.com/news/capital-business/wp/2014/03/05/why-ashburn-va-is-the-center-of-the-internet/?noredirect=on&utm_term=.aad8cd0d8ec8), and every GraphQL service seemed to be running on an [Amazon EC2 instance](https://aws.amazon.com/ec2/). After doing a little more Googling I found that [GraphQL](https://en.wikipedia.org/wiki/GraphQL) is an API development tool and has two major IDEs: [GraphiQL](https://github.com/graphql/graphiql) and [GraphQL Playground](https://www.prisma.io/blog/introducing-graphql-playground-f1e0a018f05d/). These IDEs run in the browser, much like Jupyter Notebooks, and, when running on an Amazon EC2 instance, allow you to test and develop your server's API... from anywhere. Unfortunately it seems that if you aren't careful that means that I can test and write your API from anywhere too! I picked one of the few IPs that wasn't in Ashburn, this one in San Jose, hoping that it would belong to a goofy startup.
![](/images/100Days/Day12/graphql.png)
They were running the GraphiQL IDE on this IP, just off of port 443, the https port. Now you'll see there in that screencapture I was trying to figure out how to make a query in GraphQL, and I wasn't choosing "topInfluencer" at random. GraphiQL will either autocomplete or give suggestions for terms if you hit control+space, so I found it pretty easy to start figuring out a bit about their API based on the autosuggestions it was giving me. I had more help, this coming from the IP's SSL certificate (remember that this is running off of port 443, so it has an https certificate - which unfortunately for them wasn't working which gave me the idea to check it).

```
SSL Certificate
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            03:45:9e:6a:e3:ab:8d:f2:90:d3:99:31:19:a9:e0:78:a3:e2
    Signature Algorithm: sha256WithRSAEncryption
        Issuer: C=US, O=Let's Encrypt, CN=Let's Encrypt Authority X3
        Validity
            Not Before: Nov  9 17:38:24 2018 GMT
            Not After : Feb  7 17:38:24 2019 GMT
        Subject: CN=*.staging.zipline.co
```
You can see from that last line there that this certificate is under something called staging.zipline.co. Checking out zipline.co...
![](/images/100Days/Day12/zipline.png)
Yes!! A goofy startup, just like I dreamed of. So what do they do?
![](/images/100Days/Day12/ziplineabout.png)
Oh uh... okay
![](/images/100Days/Day12/ziplineabout2.png)
Yeah okay so they connect brands to influencers to hawk their wares on Youtube, Instagram etc. Armed with this knowledge I felt free to spend as much time as I needed to figure out how to make a successful API call. And I did! Zipline is helping influencers sell products like this:

```
{
  "data": {
    "products": [
      {
        "name": "Bikini Prep Package",
        "description": "With this package I will be your all access coach for your bikini competition. We will always be in close contact and I will be available to you via text/phone and e-mail. I am very passionate about competing in the bikini division and if this is your first competition I will teach you everything there is to know about competing. I will help you decide which organization is best for you to compete in and I will help you decide on a show. I will provide your diet and exercise program. You will check in with me weekly via e-mail and provide me with weekly and sometimes bi-weekly progress pictures. I will make adjustments to your diet and exercise program as necessary. I will help you with your suit selection, and give my recommendations on your tan, hair and make-up (as I am also a licensed cosmetologist.) I will provide 2 posing lessons via skype. If you live local I will meet with you in person. Additional posing sessions are available for additional fees. If you live local I also recommend getting together with me weekly or bi-weekly for one on one training sessions (also at an additional fee.) I will provide you with your a peak week plan, as well as everything you need to know and do the day of your competition. I would love to be your coach, lets get started!",
        "price": 297,
        "opportunities": [],
        "orders": []
      }
    ]
  }
}
```
And uh like this:

```
{
  "data": {
    "products": [
      {
        "name": "Trumps Enemies",
        "description": "How the Deep State is Undermining the Presidency",
        "price": 27,
        "summary": null,
        "videos": [
          {
            "id": "756",
            "description": ""
          },
          {
            "id": "758",
            "description": ""
          }
        ],
        "opportunities": [],
        "orders": []
      }
    ]
  }
}
```
And um this:
```
{
  "data": {
    "products": [
      {
        "name": "Dangerous",
        "description": "\nThe liberal media machine did everything they could to keep this book out of your hands. Now, finally, Dangerous, the most controversy old book of the decade, is tearing down safe spaces everywhere",
        "price": 23,
        "summary": null,
        "sales": null,
        "videos": [],
        "opportunities": [
          {
            "id": "154",
            "topInfluencer": null,
            "amount": 10,
            "visibility": "Public",
            "isPercentage": true,
            "isActive": true,
            "applicants": null,
            "applicantTotals": null
          }
        ],
        "orders": []
      }
    ]
  }
}
```
Read over that last description again. Is "controversy old" supposed to be... controversial?? Yeah so basically they're scum. And they're the kind of scum that leaves their API open with user accounts and emails visible. Whoops! See you tomorrow.
