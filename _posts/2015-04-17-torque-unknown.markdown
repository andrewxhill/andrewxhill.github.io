---
layout: post
title: "More on the Torque unknown"
subtitle: "with some methods you may have missed"
modified: 2015-04-17
category: blog
tags: [cartography, torque, methods]
header-img: "img/posts/torque-unknown/header.png"
---


Classifying Torque maps is a neuron-twister. They are essentially rasters, but they regenerate based on zoom and respond to headers defined on the fly by the users. At the end of the day, they resemble much closer vector points. I dunno, they are kinda Point-based Vector Tiles... they are kinda not. At the end of the day, they are Torque and all the rest are imitators. 

If you aren't familiar with how Torque works, this [very old slide deck](http://gijs.github.io/images/cartodb_datacubes.pdf) still has some relevant information. Also review the posts of [Javi Santana](http://javisantana.com/blog.html).

## Static maps that static

Given that Torque does a great job whipping tons of points into shape, it also has some cool uses even when you don't want to animate data. The reason is that the minimum necessary data is sent to the browser to render. Two key points are **minimum** and **sent to the browser**, those are the magic keywords to the web graphics secret societies. 

Why is that interesting for **static maps**? Because unlike tile based maps, you have the data right there to do cool things with in the browser! Here is how you do it.

_For all my examples below, I'll use a dataset of tweets about McDonalds versus Burger King over a few day period. If you are doing this in the editor, before you apply the CartoCSS, you must select a Torque map from the CartoDB Editor's wizards._

**cartocss**

{% highlight css %}
Map { 
    -torque-frame-count:1; 
    -torque-animation-duration:0; 
    -torque-time-attribute:"cartodb_id"; 
    -torque-aggregation-function:"count(*)"; 
    -torque-resolution:8; 
    -torque-data-aggregation:cumulative; 
} 
#hamburgers{ 
    marker-opacity: 0.9; 
    marker-line-color: #FFF; 
    marker-line-width: 0; 
    marker-line-opacity: 1; 
    marker-type: arrow; 
    marker-width: 4;
    marker-fill: #B10026; 
    [value < 12]{ 
     marker-fill:#FC4E2A;
     [value < 4]{ 
       marker-fill:#FD8D3C;
       [value < 3]{ 
         marker-fill:#FEB24C;
         [value < 2]{ 
           marker-fill:#FFFFB2;
           }
       }
     }
    }
}
{% endhighlight %}

If you are familiar with CartoCSS in Torque, you'll notice we do a few strange things here. In particular are the first two lines of the header,

{% highlight css %}
  -torque-frame-count:1; 
  -torque-animation-duration:0;
{% endhighlight %}

The first rule, _torque-frame-count_ tells Torque to only have 1 single frame in time. The second rule tells Torque to not play the time-slider. If we used the [CartoDB.js](http://docs.cartodb.com/cartodb-platform/cartodb-js.html) to put the map on the site, we would remove the time-slider from view entirely too. I'm just going to embed the map with an iframe, so it will still be there. Let's take a look at the outcome,

<iframe width='100%' height='420' frameborder='0' src='https://team.cartodb.com/u/andrew/viz/e7fa45bc-e53b-11e4-aec4-0e0c41326911/embed_map' allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>

#### Why is it neat?

Like I said before, now the data is rendered in the client. That means we can do neat things with it. Using the CartoDB.js library, we can add events to our map and restyle or filter the data on the fly based on the values returned by our aggregation. Take a look at [this map](http://bl.ocks.org/andrewxhill/adb44dcdcf30ee449e87) for inspiration on using dynamically set Torque styles. You can also have tight control on the colors returned by each aggregation, which can be challenging using color-compositing often done on tile based maps. 


## Bubble maps that grow

Another thing I really like playing with in Torque are bubble maps. Actually, you can combine static Torque maps and bubble maps [quite easily](http://bl.ocks.org/andrewxhill/94688372b76060f7a6e8). But in this case, I'm more interested in making bubble maps that grow over time as more _events_ occur under the bubble. I first described the method in a [StackExchange ticket](http://gis.stackexchange.com/questions/129838/show-change-in-size-over-time/130114#130114) back in January, but let's revisit it here. 

**cartocss**

{% highlight css %}
Map {
  -torque-frame-count:128;
  -torque-animation-duration:10;
  -torque-time-attribute:"postedtime";
  -torque-aggregation-function:"sum(1)";
  -torque-resolution:16;
  -torque-data-aggregation:cumulative;
}

#hamburgers{
  comp-op: source-over;
  marker-fill-opacity: 1;
  marker-line-color: #FFF;
  marker-line-width: 0;
  marker-line-opacity: 0;
  marker-type: ellipse;
  marker-width: 1;
  marker-fill: #F84F40;
}
#hamburgers[value>2]{
  marker-width: 2;
}
#hamburgers[value>4]{
  marker-width: 3;
}
#hamburgers[value>6]{
  marker-width: 4;
}
#hamburgers[value>8]{
  marker-width: 5;
}
#hamburgers[value>10]{
  marker-width: 6;
}
#hamburgers[value>12]{
  marker-width: 7;
}
#hamburgers[value>14]{
  marker-width: 8;
}
{% endhighlight %}

The key parts of the CartoCSS rule set are now,


{% highlight css %}
  -torque-time-attribute:"postedtime";
  -torque-aggregation-function:"sum(1)";
  -torque-resolution:16;
{% endhighlight %}

Here is what you get,

<iframe width='100%' height='420' frameborder='0' src='https://team.cartodb.com/u/andrew/viz/e4709334-e53a-11e4-b6e6-0e853d047bba/embed_map' allowfullscreen webkitallowfullscreen mozallowfullscreen oallowfullscreen msallowfullscreen></iframe>

We explicitly set the **time-attribute** to the column in our dataset that has the timestamps to order the visualization by. This is the standard method in Torque, but we didn't need it in our static maps because we weren't replaying time in the final map. Here we do.

The **aggregation-function** is one of my favorite parts of Torque because it is actually embedded **SQL** right in our CartoCSS. It tells torque how to add up the data inside each 3D time-space pixel in Torque. Here, I just say, **ADD 'EM UP!**, since **sum(1)** will just add 1 for each row in the set. 

I'm fond of making Torque maps that use high **resolution** values. This parameter sets the height and width (in screen pixels) of each pixel in the Torque data. Here, I set it to 16, which means that all the data in each 16x16 pixel cell will be added up by our aggregation function and return the value within. Since **marker-width** is measured in radius, I set the biggest one to **marker-width: 8;** so that it fills up the entire cell. You can tell because no two markers ever overlap, just barely touch on the edge if they are both big. 

#### Why is it neat?

This method is just a stab at something interesting, I think there is a lot more to do in there. But it shows you some simple uses of aggregation functions and the **value** parameter that it returns. You can also do it with a **linear** rendering instead of the **cumulative** one I show, [take a look here](https://team.cartodb.com/u/andrew/viz/32ff4f28-7e51-11e4-9555-0e853d047bba/public_map).

## Category maps that categorize

You've probably seen a lot of categorical maps using Twitter. This [India Elections Map](http://srogers.cartodb.com/viz/81916204-c392-11e3-bcbf-0e230854a1cb/embed_map?title=true&description=true&search=true&shareable=true&cartodb_logo=true&layer_selector=false&legends=true&scrollwheel=true&fullscreen=true&sublayer_options=1%7C1&sql&sw_lat=11.821410465077479&sw_lon=60.335443281250036&ne_lat=27.525102650180578&ne_lon=99.93016984375004) is one or this [Alcatraz Escape Map](https://siggyf.cartodb.com/viz/a3f7aec6-788b-11e4-a565-0e853d047bba/embed_map) via [WashPo](http://www.washingtonpost.com/news/morning-mix/wp/2014/12/15/the-alcatraz-escapees-could-have-survived-and-this-interactive-model-proves-it/) is another. 

There are a couple of funny things about categorical maps in Torque. The first is the default use of the aggregate function (the same one we looked at above). In the typical categorical Torque map, the aggregation function is,

{% highlight css %}
  -torque-aggregation-function:"CDB_Math_Mode(category_name)";
{% endhighlight %}

The **category_name** column holds an integer for each category and **CDB_Math_Mode** returns the [mode](http://en.wikipedia.org/wiki/Mode_%28statistics%29) or category of most occurrences for each Torque pixel over time. That is fine, but it means that the color rendered is going to be _either/or_ and then blending is all funny because you may have missed pixels where there was some of each. Let's get crazy and fix this.

I saw a possible way forward in the methods described in Stamen's [Trees, Cabs & Crime](http://content.stamen.com/trees-cabs-crime_in_venice) map. Basically, we can do some nice things with color composite. Let's start with a default Torque Category map with two colors, **aqua** and **magenta**.

<a class="embedly_map" href="https://team.cartodb.com/u/andrew/viz/39444bea-e53a-11e4-805f-0e4fddd5de28/embed_map">https://team.cartodb.com/u/andrew/viz/39444bea-e53a-11e4-805f-0e4fddd5de28/embed_map</a>

_(click to load map)_

**cartocss**

{% highlight css %}
Map {
-torque-frame-count:128;
-torque-animation-duration:10;
-torque-time-attribute:"postedtime";
-torque-aggregation-function:"CDB_Math_Mode(category_name)";
-torque-resolution:2;
-torque-data-aggregation:cumulative;
}

#hamburgers{
  comp-op: darken;
  marker-fill-opacity: 0.7;
  marker-line-color: #FFF;
  marker-line-width: 0;
  marker-line-opacity: 1;
  marker-type: ellipse;
  marker-width: 6;
  marker-fill: white;
}
#hamburgers[value=1] {
   marker-fill: #ff00ff;
}
#hamburgers[value=2] {
   marker-fill: aqua;
}
{% endhighlight %}

Burger King is killing it... but there is a problem, what happens when a pixel has both values in it? It is clear that when two pixels adjacent to each other overlap we get the blending effect that makes them blue. But we need to blend them somehow using our aggregate function. Here is a simple way,

{% highlight css %}
  -torque-aggregation-function:"sum(distinct(category_name))";
{% endhighlight %}

The idea here is simple, now when all the values in a pixel are = 1, the sum of distinct is 1. When all the values are 2, the sum of distinct is 2. When the values are mixed with either 1 or 2, the sum of distinct is 3. So now we just need to color the pixels where **value=3** to be the already blended color. Here goes, 

**cartocss**

{% highlight css %}
Map {
-torque-frame-count:128;
-torque-animation-duration:10;
-torque-time-attribute:"postedtime";
-torque-aggregation-function:"CDB_Math_Mode(category_name)";
-torque-resolution:2;
-torque-data-aggregation:cumulative;
}

#hamburgers{
  comp-op: darken;
  marker-fill-opacity: 0.7;
  marker-line-color: #FFF;
  marker-line-width: 0;
  marker-line-opacity: 1;
  marker-type: ellipse;
  marker-width: 3;
  marker-fill: white;
}
#hamburgers[value=1] {
   marker-fill: #ff00ff;
}
#hamburgers[value=2] {
   marker-fill: aqua;
}
#hamburgers[value=3] {
   marker-fill: blue;
}
{% endhighlight %}

Which now looks more _mixed_, 

<a class="embedly_map" href="https://team.cartodb.com/u/andrew/viz/059b500e-e53a-11e4-b66d-0e4fddd5de28/embed_map">https://team.cartodb.com/u/andrew/viz/059b500e-e53a-11e4-b66d-0e4fddd5de28/embed_map</a>

#### Why is it neat?

What!? Why would you ask that? This is just an early stab at how to mix dynamic SQL and some really cool color compositing on the client side Torque rendering. Play with it, I'm sure you'll find some neat things here.

_There is a pretty nice way to do it with three categories too, but I'll leave that for you to work out._

## Category maps that diverge

So the ability to embed SQL into the **aggregation-function** really makes do some extreme things sometimes. The other day, I started to look into solving a new problem, _what happens when there is only one record of category 1 and ninety-nine records of category 2_? We will probably have some nice easy ways to do this in the future, but for now, the solution is actually possible with SQL and a bit of playing around. 

{% highlight css %}
  -torque-aggregation-function:"100+sum(floor(category_name*1.5)-2)";
{% endhighlight %}

I wont go into this too much, since it is a bit of a hack. But if our category_name column is either a 1 or a 2, this converts them to -1 or +1 and then sums them all up. The greater negative it is, the greater preference there is to the 1 category in the pixel, the greater it is positive the greater the preference to the 2 category. Torque doesn't return a negative value, so I add 100 to be safe. Here is the start of defining that map,

<a class="embedly_map" href="https://team.cartodb.com/u/andrew/viz/55d096d2-e536-11e4-9266-0e6e1df11cbf/embed_map">https://team.cartodb.com/u/andrew/viz/55d096d2-e536-11e4-9266-0e6e1df11cbf/embed_map</a>

**cartocss**

{% highlight css %}
/** torque_cat visualization */

Map {
-torque-frame-count:128;
-torque-animation-duration:10;
-torque-time-attribute:"postedtime";
-torque-aggregation-function:"100+sum(floor(category_name*1.5)-2)";
-torque-resolution:2;
-torque-data-aggregation:cumulative;
}

#hamburgers{
  comp-op: darken;
  marker-fill-opacity: 0.3;
  marker-line-color: #FFF;
  marker-line-width: 0;
  marker-line-opacity: 1;
  marker-type: ellipse;
  marker-width: 2;
   marker-fill: blue;
}
#hamburgers[value>104] {
  marker-fill-opacity: 0.5;
}
#hamburgers[value<96] {
  marker-fill-opacity: 0.5;
}
#hamburgers[value>110] {
  marker-fill-opacity: 0.7;
}
#hamburgers[value<90] {
  marker-fill-opacity: 0.7;
}
#hamburgers[value>100] {
   marker-fill: aqua;
}
#hamburgers[value<100] {
   marker-fill: magenta;
}
{% endhighlight %}

## Conclusions that are concluding

That's a quick brain-dump of some fun things to do with Torque. Using combinations of the aggregation method and the variable CartoCSS, you can do some pretty far out things. Give it a try!

<script type="text/javascript">

    var main = function() {
        $('.embedly_map').embedly({
          key: 'e1ded84aa14d41c7a913bc43cd0513d1',
          query: {luxe: 1},
          display: function(obj){
            // Overwrite the default display.
            if (obj.type === 'video' || obj.type === 'rich'){
              // Figure out the percent ratio for the padding. This is (height/width) * 100
              var ratio = ((obj.height/obj.width)*75).toPrecision(4) + '%'
              if(obj.width<400) ratio = ((300/obj.width)*75).toPrecision(4) + '%';
              // Wrap the embed in a responsive object div. See the CSS here!
              var div = $('<div class="responsive-object">').css({
                paddingBottom: ratio
              });
              // Add the embed to the div.
              div.html(obj.html);
              // Replace the element with the div.
              $(this).replaceWith(div);
            }
          }
        });
    };
    window.onload = main;
</script>