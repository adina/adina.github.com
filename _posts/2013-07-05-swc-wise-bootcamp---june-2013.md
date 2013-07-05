---
layout: post
title: "SWC WISE Bootcamp - June 2013"
description: "Post bootcamp blogpost"
category: 
tags: [swc, teaching]
---
{% include JB/setup %}

Last week, I had an opportunity to instruct a [Software Carpentry](http://software-carpentry.org/) bootcamp for an outstanding audience of women in science and engineering (WISE).  This bootcamp was unique for multiple reasons:  

- All participants were women -- including instructors and helpers
- It was large (~120 students + more than 20 helpers/instructors).  Each class had 40 students, 2-3 main instructors, and 6 or more helpers.
- There was a division of "skill" sections (beginner, intermediate, and advanced)
- It was specifically sponsored by [NumFOCUS](http://numfocus.org/) and J.P. Morgan both financially and with volunteers to help instruct

Our collective goal for this workshop (and all others) was to introduce students to computational skills that are useful for doing science in a friendly, construcive environment.  My personal goal for this workshop was to inspire our class with what they could learn in less than 16 hours and to promote "if I can do this, you can to" can-do attitudes. 

All in all, I'm happy to report that this was a huge success.  Nelle Varoquaux and myself were co-instructors for the intermediate class.  Nelle is brilliant and made handling any tough questions easy.  Anonymous feedback from our class suggested that everyone came away from the bootcamp having learned multiple new skills and enthused about learning more.  I'm always super happy to find that every participant would recommend us to friends.  :)  

The workshop schedule was a standard recipe for SWC.  The material for the intermediate class is on [our repo](https://github.com/swcarpentry/boot-camps/tree/2013-06-wise-intermediate).
The first day, we covered databases and shell.  The second day, we went through version control with git, python (and iPython), and NumPy.  

Here's some of the highlights of what I learned from the workshop.  

##Things that went well

###First at bat, databasing.  

Nelle and I had actually decided not to cover databases initially -- as neither of us use them that much.  A quick poll to the class indicated that more than half were interested in it, so we made a quick adjustment and had Sheeri Cabral (of Mozilla fame) instruct this as the first session.  In 4 hours, the class could do a ton of data manipulation, sorting, and querying with minimal installation headaches.  I'd never thought of running databasing as a first topic -- usually its shell for me.  But it was nice to show students with "relatively instant gratification" what they could do with a small amount of instruction.  It also set a nice foundation for other topics.

###Stickie notes

Most SWC alumni will know what stickie notes are -- students have good and bad colored stickie-note and use them to communicate how they are doing throughout the course and during exercises.  "Bad" colored stickies are the best way to get either a talking instructor's attention or a helper during an exercise.  These were very effective during our class.

###Slidedecks for instruction

Nelle used slidedecks to teach her sections -- version control and NumPy.  I've found version control to be one of the more difficult topics to teach, but the feedback we received from students is that her particular [slidedecks](http://cbio.ensmp.fr/~nvaroquaux/2013wise/git.html) were very useful.  I found that when students fell behind or were stuck, they could look at the slides and get caught up.   This was more tractable than the usual html documentation we have in our repo README docs.  Nelle's slides were also really well organized with nice examples throughout.  

###Adjusting on the fly

Given this was the first time we'd taught multiple sections, I wasn't sure what "intermediate" meant.  Both Nelle and I had to do a lot of adjustments and get feedback on "going to slow" or "going to fast".  In this class, feedback was almost always "going to slow".  I pushed pretty hard in the shell section to include automation in the shell.  And then everyone wanted to learn more but we were out of time.  This is always a difficulty with shell.  Its a lot of modules of learning that I don't do a fantastic job of tying together in the end.  I think in future bootcamps, I like the idea of having a small automation section replacing some of the shell standard material.  I tried to point out that our goal was to "enable" the class not "teach them everything" and I think that point was well-received in this audience.

###Enthusiasm

These women were amazing.  They were quick learners, asked tons of good questions, and constantly wanted more.  I loved it.  Cheesy or not - I was proud to be a woman in science amidst this energy.  I had overheard that many of the women may have not joined a "regular" (co-ed) bootcamp and that this particular set-up was amenable to newbies...but honestly, their skill levels (given, in an intermeidate class) surpassed many of my past bootcamps.

I think I've taught a handful of these workshops now.  And thankfully, I've gotten a lot better since my first one.  Its a lot easier to be enthusiastic as an instructor when you're not so nervous too!  

The helpers from JP Morgan were also incredible.  These women are highly successful (even up to near CEO-level), and it was awesome to have them with us.  Its always good to remember that all of us are volunteers but so are our employers who give us up for two days.

##Things that could be improved

###Organization

Ok, yeah, I was prepping some of my materials on the plane ride over.  Life...it happens.  This made it nearly impossible for us to coordinate between the 3 classes (beginner to advanced) so that people could float in between.  We also didn't have the space to make this really flexible.  In the future, it was noted that it would be supercool to have flexible-level modules that folks could choose -- i.e., go to advanced shell but intro Python.  

###Pacing

Our comment cards always were about 50-50, "too fast" or "too slow".  I'm happy to note that in many of our comments, we also got "too fast/slow, but I understand why it is this way."  Our class was really kind to us, no one really said anything bad.  We also tried to comment on our pace some during our instruction.

###Concept mapping how everything fits together

This was an adina-fail.  I always imagine using the magic concept map -- centered on "Best computational practices" and all the reasons we teach SWC to tie together all our instructional modules.  I almost always forget about this or more likely run out of time.  In the future, I want to make more time at the start and end of each day to do this.  

##Concluding remarks

I had a lot of fun and this was an inspirational event for me.  Many of the women were just starting to transition to doing more computation for their research and some were considering major shifts in their career to do so.  I could really relate given my history moving from experimental bench work in microbiology to bioinformatics at a computer.  Some of the women asked my advice on how to get into the field.  My best answer was to tell folks you're interested, ask for the opportunity, and dig in.  A point I made was its a good filter to remove potentially bad supervisors who aren't willing to provide such an opportunity.  

I'm thankful to WISE for personal reasons - they (through scholarships, etc) pretty much sponsored much of my undergraduate studies when my parents really couldn't afford it.   I'm grateful to Greg Wilson who saw me give one of my most horrible instructional hours ever at a bootcamp and trusted me to improve .   I'm also thankful for my mentors [Titus Brown](http://ged.msu.edu/) and [James Tiedje](http://www.cme.msu.edu/tiedjelab/jtiedje.shtml) who opened the door to me when I went knocking.  

 





 