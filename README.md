# epidemioloviz
 

## Modelling epidemics must be really hard

Inspired by this really nicely done piece in the Washington Post on "Why outbreaks like coronavirus spread exponentially, and how to flatten the curve” (https://www.washingtonpost.com/graphics/2020/world/corona-simulator/), I thought I'd have a go at doing something similar, more for fun than anything else, but my attempt to model the spread of a virus with JavaScript turned out, like a lot of those things where you start out thinking "yeah, I could have a go at that", to be a lot more difficult than I thought, and just served to re-enforce what I really already knew, which is that doing this sort of thing properly must be really really hard. 

Anyway, [this is as far as I got](epidemioloviz.html) and below there are a few things I thought about while I was doing it.


## How it works

Essentially, there are a bunch of little (5px) "people-divs" which are distributed randomly and animated to move inside a "container-div". 1 person has the class "infected" at the start of the animation and if any of the other people-divs come within 4px of the infected person they too get the class "infected" and so on. There are a few global settings like the number_of_people (300) and the animation_duration (10 secs) which are set at the start.

I then added a very simple chart to show the infections curve and display the total infected and added a couple of ways to try and affect the rate of infection: Not moving (with the class .isolated) or continuing to move (with the class .distancing) - these can be changed with a dropdown by the user. Isolation and distancing people can't be infected.


## So, what did I learn?

I'm not a very sophisticated programmer, so I accept I'll be doing all sorts of stuff wrong on that side of things, but, more interestingly there's some stuff I think I found out on a more general level.

1. Modelling how things (or people) move is not straight-forward:

I tried a few things for the animation of the people divs before settling on setting x and y "movement" variables for each person-div of -1, 0 or 1 and then adding these for each step of the animation. The result is that the people "choose" a direction (N, NE, E, SE, S, SW, W or NW), which they move in until either they bump into one of the walls of the "container" or every 750 milliseconds the setMovement function randomly changes everyones direction. 

Visually it looks ok when you run it, but, of course, this isn't how people move about at all and I'm guessing the whole premise for a good model for how a virus would spread in a population must be based on decent models of how people move. Another guess would be that how people move is virtually impossible to emulate with a simple function, so the best way to do this would be to get some actual data (from Google or Apple) and then base the model on that.

2. The number of people infected varies a lot:

Without adding any of the measures like isolation and distancing that would protect the population, i.e. just running the programme repeatedly, can generate hugely different result from 100% infection in 10 secs to less than 50% - Once upon a time, I used to know something about standard deviation and variance, but that was long ago and now I'm not sure where one would start trying to work out what the spread of results "should" be in this scenario. But, what I understood was that under my (completely wrong) model of how people move about, chance played a significant role in whether or not half the people ended up infected or everyone did (a difference of 100%). 

3. Isolation and distancing required high levels of adherence before it mattered

As an extension of the previous two points, i.e the model for movement is wrong and the standard deviation of resulting infection is high, removing people from the risk of infection didn't really affect the curve for the remaining poeple until almost everyone was protected. I'm guessing this has something to do with the size of the "container" div - i.e. a change in the size of the available "safe" space in which people are moving is only increased by a tiny amount as each person protects themselves, so this needs to be a large number before the effect is noticable, particularly as chance plays a large role. Also, isolation and distancing in this programme are identical, so that distinction is a bit pointless here.

4. More generally...

As I said, this stuff must be hard to do properly. That's the main take-away, so hats off to the professionals. 

I may (or may not) plug away at this and add some stuff about imunity or mortality, but just as a fun programming challenge, because that's all this is. 







 
