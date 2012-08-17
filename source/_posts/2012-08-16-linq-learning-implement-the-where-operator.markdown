---
layout: post
title: "LINQ Learning - Implement the Where Operator"
date: 2012-08-16 17:51
comments: true
categories: 
---

I answered a question on StackOverflow a few weeks back with a walkthrough showing how to implement the Where operator yourself, using the language features LINQ is built on. 

I'm certain I stole this example from somewhere but nevertheless, I've used it a couple times to help reduce some of the magical aspects of LINQ for new developers and I like it quite a lot, so I thought I'd post it here for posterity/eventual cleanup and detail. I leave out quite a bit in this version that could be expanded on, like exactly what "yield return" is doing in the final implementation - I may come back and fill that in when I find the time.

Say we've got an array of Things, and we want to write a method to help us figure out which of those Things are awesome. Here's one way we could do it:

``` c#
static IEnumerable<Thing> ThingsThatAreAwesome(IEnumerable<Thing> things){
    List<Thing> ret;
    foreach (Thing thing in things) {
        if (thing.IsAwesome)
            ret.Add(thing);
    }

    return ret;
}
```

Which we would then call like this:

``` c#
    List<Thing> myThings;
    List<Thing> myAwesomeThings = ThingsThatAreAwesome(myThings);
```

So that's pretty keen. We're just iterating over our list of things, seeing which of them are awesome, and then returning the ones that meet our awesome criteria. But semantically it doesn't really do it for us - our awesome filter is so awesome that we want to be able to just walk up to a list of Things and call our operator on it, as if it were an instance method on IEnumerable itself.

And so that's where *extension methods* come in. Through some compiler trickery, they give us the ability to "extend" types. So like you said, by putting "this" in front of the IEnumerable parameter of our method, we can now walk up to our list of things and ask it to filter itself like this:

``` c#
    List<Thing> myAwesomeThings = myThings.ThingsThatAreAwesome();
```

So - that's where extension methods fit in. Next is the "predicate". 

So we've got our magnificent, awesome filter, and it's great, but then we have a brain explosion: with a little bit of abstraction, that method we just wrote could be used to filter *anything*. Not just lists of Thing objects, and not just filtering on things that are awesome. 

Making it work with any type is fairly easy, we just make it a generic operator with `IEnumerable<T>`, rather than `IEnumerable<Thing>` - but making it filter on any criteria is trickier. How is the method supposed to know how to filter any type? It obviously can't - our calling code will have to *tell* it exactly what we mean by "filter" - what kind of filter we want. And so we give it a second parameter, a function pointer, that expresses just what we're after. We'll call that our "predicate", which is just a way of saying a chunk of code that returns true or false. When all is said and done, it looks a little like this. We'll rename the method to "Filter", since that better expresses what we're going for now:

``` c#
    static IEnumerable<T> Filter(this IEnumerable<T> list, Func<T,bool> predicate) {
        foreach (T item in list) {
            if (predicate(item))
                yield return item;
        }
    }
```

You can see that we're not really doing anything different from our Awesome filter method before - we're still just iterating over a list, performing some kind of check, and returning the items that pass that check. But we've given ourselves a way for calling code to express exactly what that "check" should be. 

We're basically still only doing two things: iterating over a list, and running *some kind of check* over every item in that list - the items that pass the check get passed back. Except now the method doesn't really know what the check it's running looks like - we are telling it, passing that piece of code in as a parameter, our predicate, rather than hard coding it into the method itself. We leave it up to the caller to decide what they want their filtering criteria to be. 

So at this point, we've basically got the LINQ Where operator - we can now run queries over any type of collection, all with the same method. If you've not messed around with lambdas yet, don't worry about it - just know it's a very succinct way of expressing a bit of code, which in this case is telling our filter method what we want to filter on:

``` c#
    List<Thing> myThings;
    List<Cats>  myCats;

    var myAwesomeThings = myThings.Filter(thing => thing.IsAwesome);
    var myCrazyCats = myCats.Filter(cat => cat.IsCrazy);
    
    foreach (var thing in myAwesomeThings){
        Console.WriteLine("This thing is awesome! {0}", thing);
    }

    foreach (var cat in myCrazyCats){
        Console.WriteLine("This cat is crazy! {0}", cat);
    }
```
