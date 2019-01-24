+++
title = "Shodan Stories Day 20: υηκηοωη ιδεηեτγs All The Way Down in France, Private Telephone Exchanges,  Getting Lost"
date = 2019-01-23T12:45:18-08:00
draft = false
tags = []
categories = ["100 days"]
+++

Oh what a tangled web we weave. I'm not really sure what's going on with this one or how I got here, I wanted to explore a search I had seen on Shodan called "3cx servers bcn" but now I'm trapped in a digital hall of mirrors. [3CX](https://en.wikipedia.org/wiki/3CX_Phone_System) is a private telephone exchange that sometimes runs over [VoIP](https://en.wikipedia.org/wiki/Voice_over_IP), and has servers that typically tend to run on 5001.

## υηκηοωη ιδεηեτγ on 62.23.216.99
So I looked for things running on ports 5001. One of the first ones I saw was named "υηκηοωη ιδεηեτγ" which, naturally, got me pretty interested.
![](/images/100Days/Day20/ssl.png)
Going to their IP in a browser automatically tried for https but had a certificate error, and I was really struck by the url for which their certificate had been issued, which is to say that nyc-212.odin.biz sounds fake as hell. Thanks to Azalea Banks I know that 212 is an area code for NYC so at least that checked out with the phone theme. Let's come back to odin.biz in a bit.

Proceeding along to the IP prompts a login for υηκηοωη ιδεηեτγ. The login page is very pretty, there is a beach and some birds in the foreground and some mountains in the background. Again, we'll come back to this page later.
![](/images/100Days/Day20/unknown.png)
The login looked so nice I suspected that it must have a URL.
```
👻🌵🔮 $ host 62.23.216.99
99.216.23.62.in-addr.arpa domain name pointer mail.mx.vu.
```
Aha mail.mx.vu! So this is doing email or something related. What's mx.vu? It doesn't resolve to anything in the browser. According to Shodan it's in Garden City, Kansas.
```
👻🌵🔮 $ host mx.vu
mx.vu has address 209.200.39.39
mx.vu mail is handled by 10 mail.mx.vu.
mx.vu mail is handled by 20 syno.hno3.de.
👻🌵🔮 $ host syno.hno3.de
syno.hno3.de has address 89.246.70.219
👻🌵🔮 $ host hno3.de
hno3.de has address 80.237.132.25
hno3.de mail is handled by 50 mx0.hno3.de.
👻🌵🔮 $ host mx0.hno3.de
mx0.hno3.de has address 89.246.70.219
```
syno.hno3.de and hno3.de are both in Germany, unsurprisingly. 


```
👻🌵🔮 $ host mx.vu
mx.vu has address 209.200.39.39
mx.vu mail is handled by 20 syno.hno3.de.
mx.vu mail is handled by 10 mail.mx.vu.

👻🌵🔮 $ host mail.mx.vu
mail.mx.vu has address 62.23.216.99
👻🌵🔮 $ host odin.biz
odin.biz has address 80.237.132.105
odin.biz mail is handled by 50 mx0.odin.biz.
👻🌵🔮 $ host mx.vu
mx.vu has address 209.200.39.39
mx.vu mail is handled by 10 mail.mx.vu.
mx.vu mail is handled by 20 syno.hno3.de.
```

```
👻🌵🔮 $ host mx0.odin.biz
mx0.odin.biz has address 80.237.138.5
👻🌵🔮 $ host  80.237.138.5
5.138.237.80.in-addr.arpa domain name pointer mx0.webpack.hosteurope.de.
```


```
👻🌵🔮 $ host nyc-212.odin.biz
nyc-212.odin.biz has address 62.23.216.99
```


### SSL

```
SSL Certificate
Certificate:
    Data:
        Version: 3 (0x2)
        Serial Number:
            57:31:3b:5f:6a:a1:70:58:8b:94:af:2a:87:0d:3b:bc
    Signature Algorithm: sha256WithRSAEncryption
        Issuer: C=PL, O=Unizeto Technologies S.A., OU=Certum Certification Authority, CN=Certum Domain Validation CA SHA2
        Validity
            Not Before: Nov  7 15:25:34 2018 GMT
            Not After : Nov  6 15:25:34 2020 GMT
        Subject: C=VU, CN=*.mx.vu/emailAddress=admin@mx.vu
```


```
➜  ~ traceroute 62.23.216.99
traceroute to 62.23.216.99 (62.23.216.99), 64 hops max, 52 byte packets
 1  172.19.0.1 (172.19.0.1)  9.824 ms  2.049 ms  2.665 ms
 2  * * *
 3  * * *
 4  * * *
 5  192.168.142.2 (192.168.142.2)  725.002 ms  624.450 ms  600.828 ms
 6  * * *
 7  * * *
 8  * * *
 9  * * *
10  * * *
11  * * *
12  * * *
13  * * *
14  ae-2-3209.edge5.paris1.level3.net (4.69.143.170)  918.353 ms  835.658 ms  865.845 ms
15  colt-teleco.edge5.paris1.level3.net (212.73.200.90)  817.856 ms  822.151 ms  776.249 ms
16  * * *
17  * * *
18  * * *
19  * * *
20  * * *
21  * * *
22  * * *
23  * * *
24  * * *
25  * * *
26  * * *
27  * * *
28  * * *
29  * * *
30  * * *
31  * * *
32  * * *
```
