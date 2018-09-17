---
author: alden
categories:
- Electronic Text
date: 2018-03-09
guid: https://www.alden.life/?p=313
id: 313
title: Unepic Poem
url: /2018/03/09/unepic-poem
---
When thinking of making my own poetic form I, in a fit of grandiose mania, decided that I would make my own form of generative epic poetry. Dactylic hexameter?... yes! Alliteration?... YES! Epithets?... YES YES!! Heroic narrative defining the moral values of my society?... YES YES YES!!!

Well it didn't really work out that well. The biggest problem is that narrative is really hard to pull off with generative and random-based methods. It would take a lot more time than I really had to set up the kinds of rules necessary for a marginally coherent narrative. I did end up with a couple of starts to what could be  inroads into generating epic poems. First I started out by collecting in a python dictionary all of the homeric epithets, which actually took a couple of hours because I was making it by hand. I think I'll try to add it to Corpora because they didn't have a list of homeric epithets yet and maybe somebody else would find it useful to add a little classical flourish to their language. Then I tried splicing in epithets into other texts to see if they were interesting. Unfortunately I didn't do a great job of it, I tried to use Spacy to tag nouns and proper nouns but then I could not figure out how to indicate the insertion of an epithet before the word that I had tagged. I'd like to do it but I think I'd need some more time.
Then I started a different route. I had noticed that in a lot of the epic poem translations on Project Gutenberg there were little sidebar marginalia made by the translator explaining some of the cultural references or making a little clearer what was narratively happening if in keeping with the poetic form of the original, the translation left out some of the story. By pulling these side notes out and concatenating them all together I found that I was able to build the skeleton of a narrative, albeit one that had been bleached of its interesting form and was instead a quite dry explanation of the poems' plot. This was especially true of Beowulf, because the translator had more or less added a note to every major plot point but kept his notes in something of a Shakespearian English style, with plenty of "thee"'s and "thy"'s. From that plot skeleton I was able to start manipulating, adding, and fleshing out, replacing references with new ones. I made a start in that direction also but was not particularly happy with the way it was progressing. You can see all of my work on my github [here](https://github.com/miamiww/ElectronicText/tree/master/epic_poem).
