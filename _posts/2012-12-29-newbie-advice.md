---
layout: post
title: "Advice from newbie to newbie"
description: "How to infiltrate bioinformaticians"
category: 
tags: [newbie, young scientists, advice]
---
{% include JB/setup %}

This is part II of II discussing "How to become a bioinformatician".  You can see part I [here](http://adina.github.com/2012/12/05/grownup-adina).

I spent our long holiday car trip coming up with some advice I'd give my past self when I first started dabbling in computational biology three years ago and here's what I came up with:

## 1. Commit (and stop whining)

You'd think years of experience of trying new things would prepare me that learning new things is hard, but I still get frustrated at how long it takes for me to become efficient at new adventures.  Learning to use my computer in new way and transforming into Adina2.0 was no different.  

The first thing I had to do was to commit to doing things the way I already knew how to do them and to start from ground zero.  In bioinformatics land, this meant for me to stop using my Finder (the equivalent to Windows Explorer on PCs), Excel, and any graphical-interface easy-to-use software on my computer.  

To Adina1.0, don't worry that you could have sorted that list in 10 seconds in Excel, and it took you half a day to write that sorting program because now you can sort a million lists in ten seconds and someone pays you for it.

## 2. Use the right tool for the job

Thank gawd my advisor told me to buy a Mac.  I do all my programming within a [unix](http://en.wikipedia.org/wiki/Unix) operating system which comes with a Mac.  In 3 years, I have never had to use anything else.  If you own a PC, I've heard that installing [Ubuntu](http://www.ubuntu.com/download), a unix-clone, would work well too.

There's only so much I could do on my own computer too, and I could've used a tutorial [like-this-one](http://ged.msu.edu/angus/tutorials-2012/day1.html) on how to connect to a server (usually a bigger computer that is not sitting next to you).

To Adina1.0, it doesn't matter how much more that pretty shiny computer costs, it will be worth it, trust me.

## 3. Take Command

Learn to use the "[command shell](http://software-carpentry.org/4_0/shell/intro.html)".  The best description I've gotten of the command shell is that it is the pilot's seat, its a program that's job is to run the other programs. For many bioinformatic tools, there is either only a command-line interface or a more flexible version within the command line.  It also allows you to do amazing things with existing programs, such as automate them.

To Adina1.0, on a Mac, you can access the command line from the Terminal app.  Do some googling on "command line tutorials" or check out [Software Carpentry's](http://software-carpentry.org/4_0/index.html) tutorials on the shell.  

## 4. Install and use a text editor

You can't use Word to write programs - Adina1.0 fail. Most people I know use two text editors, [vi or Emacs](http://en.wikipedia.org/wiki/Editor_war).  They were both pre-installed on my Mac (see #2).  

To Adina1.0, even though you use Emacs, be able to at least open, close, and save files in vi.  Start looking at different data files you usually use in a text editor.  Excel files are often just simple text files separated with either tabs or commas.

## 5. Learn to manipulate files

Start memorizing commands and use them regularly, list files (ls), rename/move a file (mv), copy a file (cp), read a file (cat, head, tail, less, more), etc.  Google "common unix commands" and you'll find useful resources like [this one](https://pangea.stanford.edu/computing/unix/shell/commands.php).

To Adina1.0, you can do everyting you many of the things you can do in the finder in the shell - use the shell daily for this.

## 6.  Shortcuts!

Use the [tab completion](http://en.wikipedia.org/wiki/Command-line_completion) when you type in commands.  Combine it with the wildcard character ''\*'' and [pattern matching][1] to make things really fast. 

If you login into a server, learn to use a [config file](http://ivetetecedor.com/207/how-to-set-up-an-ssh-config-file-in-mac-os-x).


[1]: http://en.wikipedia.org/wiki/Glob_(programming)

To Adina1.0, write down all the nifty shortcuts you learn somewhere for a blog 
in the future as you use them so often now you can't even remember them.

## 7.  Learn a programming language

There are so many to learn, and some are easier than others.  There are also tons of tutorials on beginning to program if you know how to use Google to find them.  I generally can search for i.e., "python tutorial" and start clicking through links until one hits the spot for me.  In Software Carpentry, we teach students in Python tutorials like this [one](http://software-carpentry.org/4_0/index.html#python). If you get a chance to attend one of these Software Carpentry workshops, its a great accelerator for learning how to become better computational scientist. 

 Tutorials I used are:  [the classic](http://docs.python.org/2/tutorial/) and [this book](http://www.amazon.com/Bioinformatics-Programming-Using-Python-Biological/dp/059615450X/ref=sr_1_2?s=books&ie=UTF8&qid=1356819689&sr=1-2&keywords=python+bioinformatics). 

 Here are some more that looked interesting, a free [Google class] (https://developers.google.com/edu/python/) and [a fun interactive one](http://www.learnpython.org/).

To Adina1.0, pick up Python, its awesome.  More important than reading is just doing.  Just write a program daily for a month. Write down ten things you do with excel and then do that with Python (i.e., alphabetize a list, sort by the 5th column, find and replace a word, find the average and standard deviation, copy a file to another file with slight changes on each line, switch from tab delimited to comma separated outputs, etc.).  Use two terminal windows, one for writing the program and one for executing and put them side by side.

## 8.  Become addicted to print statements 

If you're not sure what your program is doing or even if you are, put print statements in printing out relevant outputs of your program.  And because you're printing things out, make sure you test programs on simple tasks or small files first.


    list = []
    for i in range(0,3):
        print 'i=', i
        for j in range(0,3):
	    print 'j=', j
            print 'i*j=', i*j
            list.append(i*j)
            print list
    print 'the final', list

To Adina1.0, write the program for yourself first and always test on a small file.


## 9. Do something relevant.

Find an interesting biological question for yourself, research the tools you need to start answering it, and go at it!

Read the manual. If there is no manual, look for a file called the README file and read it (see #5).  Go through the install and execution.  

Look at the inputs and outputs to the program.    

One of the most used bionformatic tools since its essentially our "biology thesaurus" (i.e., finding similar organisms within a database) is BLAST.   

Here is our [tutorial](http://ged.msu.edu/angus/tutorials-2012/files/static-ngs-10-blast.html) or [tutorial-not-in-ipython](http://ged.msu.edu/angus/tutorials-2011/running-blast.html) on using it and manipulating its output. (Random advice: Just copy and paste commands following but not including the "%%" in gray.)

To Adina1.0, if you can't install a program on your computer, try it on a clean install of unix on a server using Amazon EC2.  If you can't get it on there, find a friend to help because that's what they are there for.
 
## 10. Start automating.

This is an advanced move but maybe one of the most rewarding as its when all the inefficiency in learning pays off big time in high throughput amazing glorious ways.  

Start by learning about how to write a for loop on the command line, amd you'll be well on your way to start automating processes.  I started by looking at these tutorials [Bash for Loop Examples](http://www.cyberciti.biz/faq/bash-for-loop/) and [Easily renaming multiple files](http://www.debian-administration.org/articles/150).  Again, I use google a-l-o-t with searches like "for loop on command line".

To Adina1.0, name your files something that makes sense and with consistency.  Keep them organized as-you-go and happy automation may proceed.

## You can do it!
The best advice I have to folks interested in getting into bioinformatics with no training is just to start with a good attitude and commitment.  Ask for help when you're stuck because we were all there once too.

Hope this helps!  Happy holidays and Happy New Year!
~adina