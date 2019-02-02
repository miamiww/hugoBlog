+++
title = "Shodan Stories Day 29"
date = 2019-02-01T23:01:04-05:00
draft = false
tags = []
categories = ["100 days"]
+++

I saw someone searching for "ICO". At first I thought maybe it had something to do with the [groundbreaking 2001 indie game](https://en.wikipedia.org/wiki/Ico), but after browsing some links I realized that no, it meant ["Initial Coin Offering"](https://www.investopedia.com/terms/i/initial-coin-offering-ico.asp), and yes this is another crypto thing.

## CoinCircle's ICOStats Tracker on 165.227.6.170
Most of the results on Shodan are websites and webservers, but I found one running on Digital Ocean that's just a web app running on port 3000.
![](/images/100Days/Day29/icostats.png)
The app is called ICO Stats, and appears to collect and display real time information about a whole lot of different "coins". Digital coins, digital tokens, digital assets, what are these things? I believe I have a fairly decent grasp of the mechanics of creating them, but what I don't understand is how the market works and how value is being assigned. Is the demand just entirely speculation?
![](/images/100Days/Day29/performers.png)
Look at that! There's a coin called NXT whose value has increased _173940%_ in the past 4 years. That means that if you bought a single dollar of NXT in 2013 you would now have nearly _one hundred and seventy four thousand dollars_ worth of it now. Crypto world feels like an entirely different vision of reality, one that makes me queasy and filled with disgust.

It didn't take me long to figure out who had created this tracker application.  First I found their [Trello board](https://trello.com/), the last addition to which was yesterday.
![](/images/100Days/Day29/trello.png)
From there I found linked the [github](https://github.com/CoinCircle/icostats), and that led me to [Coin Circle](https://coincircle.com/).
![](/images/100Days/Day29/coin.png)
Coin Circle is a company(?) that will help you tokenize your assets to decentralize your chain of trusts and connect you with savvy accredited buyers on the digital platforms of tomorrow, today. Or maybe it's just only on their digitally decentralized platform based distributed ledger system.
![](/images/100Days/Day29/tokenize.png)

I'm making fun, but I'm genuinely against what they are doing. Maybe my futurevision is a little clouded but to what end are we creating this additional layer of abstraction? Who benefits from the tokenization of an asset? Who loses? Who has control? The "market"?
![](/images/100Days/Day29/roguegallery.png)
Probably just people like this rogues gallery. See you tomorrow.
