+++
title = "Shodan Stories Day 45: Filferro in Empuriabrava, .NET Games, eMule, Pokémon Armageddon, and the Joy Only Known to Those Who Keep Their Campsites Cow Free"
date = 2019-02-17T17:56:03-05:00
draft = false
tags = []
categories = ["100 days"]
+++

Another day another search. Today I found a shared search for "emule". "What's an emule?" I asked myself, and dove into the search.

## An eMule on 87.216.176.220
[eMule](https://en.wikipedia.org/wiki/EMule) is an "electronic mule", duh. It's a kind of peer to peer software, different from bittorent, but I'm not sure exactly how. Every explanation I've found on how it works is a bit over my head, or at least over my attention span. It seemed like eMule was mostly popular in Europe, and I picked a result in Spain with eMule running on port 8000.
![](/images/100Days/Day45/firstlook.png)
eMule has a truly incredible mascot. Unfortunately there is not a ton to do with eMule since it requires a login. I did find, however, that this IP was also running a normal web page on port 80, with the domain name "filferro.cat".

```
➜  ~ host filferro.cat
filferro.cat has address 87.216.176.220
```
![](/images/100Days/Day45/filfero.png)
This appears to be the portfolio page of a very unusual indie game designer. Someone who eschews easy out of the box game engines, common programming tools, and newfangled gameplay mechanics. No, this person prefers to get back to the basics, back to the real, making Windows XP games with [.NET](https://en.wikipedia.org/wiki/.NET_Framework) and [Visual Basic](https://en.wikipedia.org/wiki/Visual_Basic)
![](/images/100Days/Day45/pokemon.png)
That game description is in Catalan but I'll translate for you.

>__Introduction__

>Coming from the outer space, fearless foreigners dressed in Pokémon attempts to live in peace and freedom and, above all, respectful of the constitution of our beloved planet Earth. The World Government, headed by the insigne Josep Maria Asnar, sends you with a clear mission: to destroy the aliens - Pokémon ... because as our constitution says: "Everyone who is against the constitution is an alien - Pokémon "

>__Technical characteristics__

>Game of ships where it will be necessary to end the aliens - Pokémon. The game has been developed in Visual Basic ™ (it is installed with the Visual Basic ™ dll ) and is accompanied by the source code.
You can save and retrieve games and set the game.

Yes you play as a space shuttle and your goal is to shoot little invading Pokemon sprites with your space shuttle laser gun.

There is also a game named Wet Camps.
![](http://87.216.176.220/images/games/Campes.jpg)

>Wet camps

>_Based on real events!_
The rain has become the enemy of the camps.
Tents are shattered and you will need to go from colonies!
Perhaps with the help of an umbrella we can save the situation ...

There are about a dozen all equally delightful games, with varying levels of copyright infringement, from a game about picking mushrooms that's a knockoff of [Minesweeper](https://en.wikipedia.org/wiki/Minesweeper_(video_game)) (don't pick the poisonous ones!) to a truly bonkers version of Tetris.
![](http://87.216.176.220/images/games/ifn-Tris.jpg)

My favorite my actually be another one of their camping based games, this one named, in what I can only hope is a nod to Game of Thrones, Game of Cows.
![](http://87.216.176.220/images/games/Tifa.png)

>__Introduction__

>_Based on real events!_

>Our friends, cows do not understand rental or camping contracts, nor do they know that it is a relaxation (even if it is splendid). It is necessary, then, to stomach them without slicing the stores or tamping us into the campsite.
We invite you to an exciting adventure, after some cows "bojes" ...

>__Technical characteristics__

>It is about pushing the cows out of the campsite.

Truly back to basics stuff here. Video games stripped down to their bare elements: cows, falling blocks, Pokémon. Seeing these games brought back memories of playing Minesweeper for _hours_ as a child, of eating a grilled cheese on a rainy day and just sitting and playing Oregon Trail and _fucking Minesweeper_ all afternoon. How have we strayed so far from the light?

See you tomorrow.
