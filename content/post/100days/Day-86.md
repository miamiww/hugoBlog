+++
title = "Shodan Stories Day 86: Graphing Databases in Sydney"
date = 2019-04-05T18:04:01-04:00
draft = false
tags = []
categories = ["100 days"]
+++

About a week ago I saw a search for "dgraph" and I thought today I would take a look. [Dgraph](https://dgraph.io/) is a kind of [graph database](https://en.wikipedia.org/wiki/Graph_database), which is a kind of NoSQL database with a graph-like structure of nodes and edges. The search was for "Dgraph Ratel Dashboard".

## Dgraph Server on 13.210.169.101
There were only 5 results, all either in China or Australia, and so I picked one in Australia because Dgraph is based in Sydney. It was running the Dgraph dashboard on port 8081.
![](/images/100Days/Day86/firstlook.png)
There wasn't actually a lot I could do here. It didn't ask me for authentication or anything, there just wasn't any data. All of the results I found seemed this way actually.

According to an [article I read, Dgraph seems to be reasonably popular](https://techcrunch.com/2017/12/19/dgraph-raises-3m-for-its-open-source-distributed-graph-database-hits-1-0-release/), so I assume that I only found these few results because anyone who actually has data has better secured their system so that they don't show up on Shodan.

Good thinking on their part. See you tomorrow.
