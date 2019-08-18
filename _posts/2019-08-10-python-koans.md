---
layout: post
title: "Python Koans, Spaced Repetition, and the Pomodoro technique"
author: "Cristina Elep"
tags: [python, pomodoro, 'spaced repetition']
---

So far I've been using the following tools to learn Python 3; they seem to work well together, though I could probably fine-tune my study habits further.

## Python Koans

The [Python Koans](https://github.com/gregmalcolm/python_koans) are a TDD-based tutorial for learning Python; you clone or fork the repository, execute the runner script, then incrementally get all the tests to pass by either supplying the correct expected value or writing some code. It's a port of the [Ruby Koans](rubykoans.com), which I haven't tried yet; based on my experience with the Python version so far, the Ruby Koans would have been helpful when I was first learning Ruby. Passing tests are a great way to record what is considered true for a codebase, or in this case the language itself -- all you have to do is run the test suite to see what works and what doesn't, assuming you've got those bases covered.

## Spaced Repetition

I learned about [spaced repetition](https://en.wikipedia.org/wiki/Spaced_repetition) via an [interactive tutorial/comic](https://ncase.me/remember/) by Nicky Case. I initially started using it to memorize Japanese kanji; when it seemed to be working really well, I started using it for other things, like memorizing dictionary words and (re-)learning JavaScript basics. I only started my (almost) daily memorization exercises around a couple months ago, so I don't have a lot of data, but it currently seems to be an effective learning method for me. So when I started learning Python 3 I included it in my learning toolbox.

Spaced repetition involves converting information into flash cards, either physical or digital, which you then review according to a schedule. Nicky Case's tutorial shows how to build and use a physical [Leitner box](https://en.wikipedia.org/wiki/Leitner_system) with 7 levels for storing and scheduling the flash cards; basically, you start with around 5-10 cards in level 1, then when you've memorized them they go up one level. You add more cards every day, and you review your cards every day according to a predefined schedule/algorithm; the higher the level a card is in, the less frequently you have to review it. Cards that "graduate" from the highest level are retired for good.

Here's an example of a card I made that uses [cloze deletion](https://en.wikipedia.org/wiki/Cloze_test), with information taken from the Python 3.7.4 documentation:
```
front:

by default, Python source files are treated as encoded in ___
(Unicode, one to four 8-bit bytes)

back:

UTF-8
```

There are also apps available that automate the creation and scheduling of cards, like [Anki](https://apps.ankiweb.net/), but I haven't tried them yet.

## Pomodoro Technique

I'd heard about the [Pomodoro technique](https://en.wikipedia.org/wiki/Pomodoro_Technique) before, but I didn't think of trying it until now. I've been using it to help me focus on the Python Koans and to force me to take regular breaks.

The technique hinges on using a timer, either a physical one like a kitchen timer or a digital one, to demarcate each "pomodoro", or work interval. Traditionally each pomodoro is 25 minutes long; when you finish one, you take a 3-5 minute break, then start the next one. Once you've accumulated a set of 4 pomodoros, you can take a longer break that lasts 15-30 minutes before starting the next set. Interrupted pomodoros don't count, although it's okay to briefly note down something to be dealt with later if it comes up while a pomodoro is still ongoing.

So far I've had some trouble maintaining focus, especially when I pause to look up something in the Python 3 docs, or on Wikipedia. Nevertheless tracking pomodoros, even interrupted ones, has been helpful in terms of figuring out how long it takes me to finish working on one of the Python Koans, or reviewing my spaced repetition cards.

## Additional Links

Nicky Case's interactive comic links to the following resources about spaced repetition:

* [Augmenting Long-term Memory](http://augmentingcognition.com/ltm.html), by Michael Nielsen -- Nielsen describes how he used Anki to do things like memorizing a subset of Unix commands (and thereby become better at using the command line) and thoroughly reading a research paper about a system he didn't know in preparation for writing an article about it

* [Effective learning: Twenty rules of formulating knowledge](https://www.supermemo.com/en/archives1990-2015/articles/20rules) by Piotr Wozniak -- Wozniak outlines 20 rules for creating effective cards, with examples illustrating the differences between effective and ineffective ones
