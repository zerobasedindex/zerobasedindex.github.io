---
layout: post
title: My Goto Interview Questions
---

## Trade Secrets

In [a previous post]({% post_url 2015-02-25-How-I-Perform-Interviews %}), I discussed how I liked to approach an interview with a technical/engineering candidate. I realized afterwards, that I didn't really provide much in the way of example questions, which brings us to now. Do what you will with these, I am not responsible if you make someone cry.

Also, most of my interviewing has been around Java developers so I'm going to use that as my goto in examples as I need to pick something concrete. But, you should be able to adapt/come up with similar questions for your intended, no doubt believed to be superior, technology.

## Basics to Formulating a Question

**First, make sure it's geared towards the level of the candidate.** Don't necessarily ask a Senior programmer with a master's degree about basic object-oriented principles. Ask them about more complex ones like _"inheritance vs composition"_, _"why does Java not allow multiple inheritance"_, or better yet, _"how can you fake multiple inheritance in Java."_ The flip side, don't ask a Junior about _"optimal database relationships"_ or _"what is third-normal form."_

**Second, if it's an open question, always ask for multiples.** For example, take the canonical _"What's your biggest weakness?"_ and change it to _"What are your three biggest weaknesses?"_. Most people have one canned answer, most people don't have three. It gets a candidate thinking on their feet instead of reciting a script. Personally, I don't care for that question but it does apply in other situations. For example, _"Name three JavaScript client-side frameworks?"_, _"What are three differences between Java and C++?"_, and _"Can you name and describe at least three design patterns?"_.

**Third, harder questions should be adjustable based on the candidate.** The best way I've found to separate the stereotypical good and great candidates is by starting with a base question and then having multiple audibles I can call based on how well the candidate has done so far. For example, I'll start with _"How would you go about accessing a private field in a 3rd-party Java class?"_. This question is deliberately vague when it comes to where this third-party code is coming from. If the candidate stumbles/pauses, I can lead them with, _"Say we checked out the code from a GitHub repository."_, hinting at the fact we have the source code. Hopefully though, the candidate is already thinking/asking about if they have access to the source or not. 

Once they are on the "having the source code path", see how they deal with modifying it. Ask them how they would document the change, or how they would handle the dependency being downloaded automatically by the build system, etc. If you want to turn the screws more, say you don't have the source code and see what they do. Again, prompting if they need with hints about decompilation, aspect-oriented programming or Java reflection. Hopefully you get the idea, I find the questions that can lead me down a path help me assess a candidates technical and problem solving skills.

**Lastly, don't ask contrived, overly-brain teasery questions.** They don't work (see [here](http://www.businessinsider.com/15-google-interview-questions-that-used-to-make-geniuses-feel-dumb-2012-11) and [here](http://business.time.com/2012/10/23/no-brainer-brainteaser-job-interview-questions-dont-work/)) and can really make your candidate feel like an idiot, which can ruin the rest of the meaningful part of the interview. I've been tempted to walk out of interviews when asked these types of questions. Just don't use them.

## Opening/Ice Breaker Questions

* So HR tells me you are here to interview for position $POSITION? Is that right? _(You'd be surprised at what HR sends you sometimes isn't what you've been told you'll be interviewing.)_
* How did you hear about this position?
* What do you know about our company?
* Can you give me a five minute pitch about who you are, what you've done, why you're looking for a new position, and what you want in this new position?
* Did you enjoy going to $SCHOOL? What did you like about it? Why did you decide on $SCHOOL?
* What were your top three courses from an enjoyment perspective (in-major if possible)?
* I see you participated in $CLUB/$ACTIVITY while there, can you tell me a little about your involvement?
* What were some of the things you liked most about working for $PREVIOUS_COMPANY?
* What are you looking to do and what responsibilities do you wish to have in your next role?
* What are some of the reasons you are looking to leave your current position? _(This one is important to me as it gets to motive and sometimes reveals a bit about their personality.)_

## Lighter Technical Questions

* What are your top three academic/professional accomplishments?
* What aspects of $LANGUAGE do you like and dislike?
* What are _some introductory components/aspects of the target language_?
  * What are the access modifiers for Java?
  * What does a constructor function do in JavaScript?
  * What is the purpose of the `__init__.py` file in a Python module?
* What are _some components/aspects of the target framework_?
  * What roles do activities, fragments, services, and intents play in Android?
  * What's the difference between a .xib and a storyboard in iOS and when would you use one over the other?
  * What do directives accomplish in Angular?
* What are _some common issues in your target environment_?
  * How do you handle crash reporting in Android/iOS?
  * What are some of the downsides to using client side rendering of the UI?
  * How do you deal with delays in mobile networking?
* What SDLC have you used? What do you like/dislike about them?
* What git branching strategies have you used?

## Heavier Technical Questions

* What's your approach for debugging non-trivial bugs? _(This is a good lead them down the path question, devlop vs prod, bug seen by customer, not reproducible, etc.)_
* Can you walk me through how you design a _component of your target framework_?
* How do you _something beyond the hello world tutorial_?
  * How is inheritance handled in JavaScript?
  * How does iOS handle memory management? How has it evolved since you've starting programming for iOS?
  * How do you enable two separate Android apps to share data?
  * What do you have to do when creating an app for separate device profiles (phone vs tablet vs laptop)?
* What goes into _doing related tasks_?
  * How do you setup a server to handle web requests?
  * How to you use SSH to enable remote access to services?
  * Can you walk me through the process of setting up a git repository?
  * What types of security need to be in place before this goes live?
* Given _problem X_, how would you solve it? _(Again, good path question, I like to reference my current or recent set of incurred problems to see what they would've said if I told them about my problem as I would a co-worker.)_
* How do you approach learning a new code base? What specific techniques do you employ to facilitate the process? _(path question)_
* Can you provide three examples of when you realized you needed help and how you came to that realization? How did you seek help? _(path question)_

## General or HR-like Questions

* How do you prefer to interact within a team? Solo vs Team in general?
* What originally attracted you to this type of work?
* Do you have any worries or reservations about working here?
* What has driven your career decisions thus far?
* Do you play disc golf?

## Wrapping Up

That's pretty much the process I use to generate my interview questions. Sometimes I'll steal questions from my co-workers when I hear them ask a good one. Other times, I just like to surf blog/GitHub articles to see what people are saying to prepare for, so I know what to use or sometimes even avoid. Good luck!
