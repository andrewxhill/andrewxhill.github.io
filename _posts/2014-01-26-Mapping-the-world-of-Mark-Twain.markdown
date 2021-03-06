---
layout: post
title: "Mapping the world of Mark Twain"
subtitle: "A fun weekend project to map every location ever written about in published works by Mark Twain."
modified: 2014-01-15
category: blog
tags: [Mark Twain, mapping, stories, data visualization]
header-img: "img/posts/world-of-mark-twain.png"
---


### Background

I was recently walking down the street with a good friend of mine. It was really late at night and I was doing what I often do in those situations, filling his ear with some story or another. It about some crazy thing I had done once and my hands were flailing a lot and I was getting really loud on the quiet streets. I love telling stories. After I was done my friend made a comment. It isn't anything new exactly, I've just never heard someone say it after listening to a story I was telling. My friend began talking about how life is short and how we are all sooo limited in the places we can go or the things we can see. He talked about stories being a cheat in life, letting you go places and be a part of situations you would never be able to in your own life. He made the argument that, to the brain, stories are as good as the fountain of youth.

### Fountain of youth

The idea is a really interesting one and so it lingered in my thoughts. Really though, it's fundamental. Heck, that's the thesis of [Reading Rainbow](http://en.wikipedia.org/wiki/Reading_Rainbow)! Still, I got really excited by thinking about storytellers and their descriptions of the world. So many stories are dotted with the street signs and mountain peaks of the real world. Take the [Odyssey](http://en.wikipedia.org/wiki/Odyssey) for example, the story is like a giant written map that takes you to the reaches of the Mediterranean sea. The story IS the map! 

What I really want to do is understand that interplay between the two. How are maps stories? And how are stories maps? I thought it would be interesting to start literally and to turn a few stories back into real maps, to actually take the written words of authors and create dots and lines that we can view. So, I began looking for some datasets about localities in books. 


### Mapping Mark Twain

This weekend I was looking through [Project Gutenberg](http://gutenberg.org) and found something even better than a single book, I found the complete works of Mark Twain. I remembered how geographic the stories of Twain are and so knew immediately I had found a treasure chest. For the last few days, I've been parsing the books line-by-line and trying to find the localities that make up the world of Mark Twain. In the end, the data has over 20,000 localities. Even counting the cases where sir names are mistaken for places, it is a really cool dataset. What I'll show you here is only the tip of the iceberg. I put the results together as an [interactive map](/maps/writers/twain/index.html) that maybe will inspire you to take a journey with Twain on your own, extend your life a little.

#### [Click here to explore the map](/maps/writers/twain/index.html)

[![](/img/posts/twains_world.png)](/maps/writers/twain/index.html)
Every location written about by Mark Twain, connected in order

[![](/img/posts/twain_usa.png)](/maps/writers/twain/index.html)
Close-up of locations in the United States

### About the map

Use the menu to select each published work by Mark Twain or look at them as a whole. You can also toggle between the line map and an interactive point map that will give you links to the passages.

I built the map using [CartoDB](http://cartodb.com) and all data came from [Project Gutenberg](http://gutenberg.org). If you want to start making your own maps, CartoDB is free to try and I've made a bunch of [tutorials for you to get started](http://developers.cartodb.com/tutorials.html). 

