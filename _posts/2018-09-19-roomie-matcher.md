---
layout: post
title:  "UCLA Roomie Matcher"
date:   2018-09-19
image: roomie-matcher.jpg
---

### Summer 2017 was about to start and I still didn't know who my college roommates would be.

I was still in high school, working away in Science Olympiad, trying not to pay attention to election results, the usual. The deadline for choosing your roommates was approaching, and I still didn't know who I wanted. I had joined the Facebook groups for UCLA class of 2021, ([I even made one for the Engineers of 2021](https://www.facebook.com/groups/uclaeng2021/)), and had mingled online with a lot of people, but still didn't really know who I would be a compatible roommate with.

> A lot of people settle with having two random roommates selected for them, but I thought that was too risky. It's not that I don't like adjusting to other people, I just didn't want to risk being placed with someone I really didn't like.

So I was thinking about what I could do to solve this problem.

## What UCLA gives you

I thought about the questionnaire on the UCLA housing website that allows their algorithm to pick people who might be compatible. It asked questions about how early/late you sleep, your policy for overnight guests, your preferred room temperature, etc. I thought they were good questions, but there were only 8 of them, which I didn't think was enough.

### Solution?

I decided to create my own roommate matcher web application! That way, I could advertise it to the UCLA Facebook group (which had thousands of members), and people could fill it out, and find compatible roommates.

#### Mini-uups

Well I was talking with my friend Nikhil at the time about this and he wanted to help, but he was an experienced Python programmer with knowledge of how to make a full solution with one application, and I was a guy who knew what a `<div>` tag was.

We discussed some ideas, but accidently made two different applications that we weren't able to consolidate. Sorry Nikhil!

## My Web App

In any case, the app I came up with was the following:

### 1. Google Form

I created a [Google Form](https://docs.google.com/forms/d/e/1FAIpQLSfObmV57LJD9cawRIhbO7XlvK0ri15DnwAtX7qzi3oGnTjOzg/viewform?c=0&w=1) in which people would answer questions about themselves. It had the same 8 questions as the UCLA questionnaire, but I added 4 questions about personality (using the Myers-Briggs personality classifier). I also added a field where you could state your hobbies (which is a big factor in who you become friends with). I didn't know about Natural Language Processing or anything like that, so I only collected this data and showed it in the resulting table; it didn't play a role in calculations.

### -> 2. Google Sheet

I then collected the data from this Google Form into a Google Sheet. I repeatedly had to clean out the sheet because someone decided to troll me by making hundreds of fake entries, each one with a random name and gender, and with hobbies as a separate line from a book. I didn't bother looking up which book it was, I just deleted all the fake entries.

### -> 3. Numpy + Pandas (Python) script

I then routinely downloaded this spreadsheet and run a Python script to analyze the data and output a table with the coefficients of compatibility of each pair of people. I did this by basically calculating the difference in answer for every answer for every pair of people, and dividing that by the maximum divergence of compatibility (which came out to something like 36). I used Numpy to do the calculations, and Pandas to output the resulting table.

#### Huh?

Ok I just said a lot of fancy words up there but keep in mind that this is my FIRST experience with Python. I literally didn't know of the language's existence prior to this project.

> I was just searching the problems I needed to solve, and found a patchwork of Python tutorials that seemed to have the right idea, so I basically said to myself: *alright I guess I'm going to learn Python now*.

### -> 4. Manual Upload (???)

Ok now after I outputted the coefficients to a table, I **manually uploaded** said table to a publicly accessible Google Sheet (I replaced all the content each time).

### -> 5. Website with Google Charts API

After that, I built a [**barebones** HTML website](https://kimeiga.github.io/ucla2021/) in which you type in your name to an input field and hit Enter, and it has a JavaScript function attached that uses the **Google Charts API** to query the public Google Sheet for the column of coefficients that corresponds to the name of the person entered. It also brings in the column for everyone's name, gender, and hobbies, and *orders everything from greatest coefficient of matching to least*.

#### ...bruv

So I know what you're thinking. Wow, what an incredibly convoluted way of doing things! You could have just used Flask and MongoDB and Bootstrap and React and Webpack and Node.js and XYZ and ABC in order to create all of this yourself and it would follow X, Y, and Z web standard while also being accessible via the keyboard and making your mom happy and--

OK, ok. I didn't know what **any** of those words meant at the time, and I honestly suspected it wouldn't have to be this hard.

## Result?

> But it worked!

I posted on the Facebook page each time I uploaded the latest spreadsheet. These posts got lots of responses and prompted people to fill out the form more and more.

> In total, about 600 people used this app

### My experience

And it was useful! Every so often, I would put in my name and see who I matched with. I would go down the list of "males" and message the ones with hobbies I liked. They would say that they were open to rooming with me, or that they're already rooming with someone. I kept looking around like this, and eventually got a list of people I liked. 

Then I let my mom look at each of those people's profiles **because that's what Middle Eastern moms do**. We eventually whittled it down further, and I eventually found my amazing roommates John and Will. We used Google Hangouts to video call each other a few times between class, and eventually decided on each other. And honestly they are such fantastic roommates <3!

#### Could I have done it without Roomie Matcher?

What struck me was that I hadn't met them online prior to seeing their name on the roommate matcher. So that means that if I didn't make this application, I probably would be roomming with someone else, and it might not have been as enjoyable or relaxed.

### Others' Experiences

I also am told by numerous people at UCLA that they met through the Roommate Matcher, which brings joy to my heart! Some have said that it actually aided them in finding a roommate, while some have said that it just helped them find friends! Honestly I was completely ecstatic when I heard those stories, and I'm glad my work has helped people transition to college.

So that's the story of Roomie Matcher! Perhaps I'll talk to the UCLA Housing Department about it! It could be a good thing for them to integrate into their system!

