---
layout: post
title: "Weekend Faffery"
date: 2012-08-23 18:54
comments: true
categories: [backbone, leaflet, instagram, faffery]
---
##Backbone+Leaflet+Instagram = Instamapstagram
<iframe width="640" height='480' src="http://iirvine.github.com/instamapstagram/index.html" frameborder="0"></iframe>

As part of a weekend-long "clear out the cobwebs" dive back into backbone, I threw together a little sample app to plot Instagram photos on a map. 

Drag the circle to kick off a search, click the little crosshairs to zoom to your location, drag the photo markers themselves to get a better view, etc etc. It's missing some basic functionality, like popups for the photos, that I may or may not get around to adding. Uses Stamen's beautiful toner tiles to a fairly nice effect - I like the counterpoint of the very minimal, black and white-ness of the basemap and interface with the colorful Instagram photos.

[This](http://www.mapgrams.com/) has been [done before](http://www.mapstagram.com/), most recently by [Instagram itself](http://blog.instagram.com/post/29555443184/instagram-3-0-photo-maps-more-weve-been); all the same, it struck me as a fun little thing I could bang out in a weekend to reinvigorate the backbone portions of my brain. 

It was quite a useful excercise - I went into it with the goal of shooting for reusable, modularized components, and ended up having to think very carefully about how that could be achieved using backbone against another library like Leaflet. 

By the end of the sprint, some concessions were being made in the interest of seeing every map maker's most favorite thing - some points on a map - but I think with a little refactoring it could be a good jumping off point. 

It's also raised some questions on just how to stuff more functionality into a map driven application without going too crazy on the interface. I like the simplicity of the full screen map - and the fact that with Leaflet it works on mobile devices right out of the box - but that kind of puts an upper limit on just how intricate your interface can get, unless you start getting creative and hiding bits of it in a container. I guess sooner or later I'll have to start experimenting with mixing in some other elements, especially since that kind of subview rendering in backbone is something I want to practice, but for now I'm kind of liking the minimal approach.

The whole excercise has led me to think that Instagram + maps is an interesting combo that would be fun to play around with some more. Off the top of my head, I can see that this app would be quite a bit more useful if it had some notion of time - some way to refine your media searches not just by location but date as well. Then you could do something like drop the circle on a festival you went to last week and see some other photos from it. It'd also be nice if I could just see all of *my* photos on a map, maybe with some kind of density visualizing [heatmap](https://github.com/sunng87/heatcanvas). And boy would I really like to play around with their [realtime API](http://instagram.com/developer/realtime/)… all in good time I suppose. 

Anyway, the code is all on [Github](https://github.com/iirvine/instamapstagram) so if you've read this far, feel free to fork away should the spirit take you.
 