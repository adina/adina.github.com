---
layout: post
title: "Lessons from ASM 2013 Denver"
description: "Recap from 2013 American Society of Microbiology General Meeting"
category: 
tags: [metagenomics, meetings,]
---
{% include JB/setup %}

The 2013 ASM general meeting in Denver was one of the best ASM meetings I've attended.  I thought I'd write about some of lessons learned from it.  

### Clear leaders in analysis workflows continue to deliver
One of the most useful sessions for me was the pre-meeting workshop "Metagenomic Approaches: Frontiers of Annotation and Assembly, Networking and Discovery" which should've been entitled "QIIME domination and then some".  More than half of the speakers are/were from Rob Knight's lineage of awesome scientists.  It was quite clear that QIIME has really "won" the game in 16S rRNA analysis and they demo-ed many of their new spiffy tools with some nice explanations of different workflows.  They haven't uploaded their presentations onto the workshop website, but I was told they would (here's the [link](https://sites.google.com/site/asmmetagenomicsworkshop/)). 

The workshop included some really nice talks from David Needham (Jed Furhman's group) on network analysis with Cytoscape, James White of CloVR-fame (a start to finish easy-to-use analysis workflow on free-for-academics DIAG computing), and Matt Sullivan and Bonnie Hurwitz on viral metagenomics (including a very nice iPlant tutorial).  Murat Eren also gave a good talk on why current 16S analyses are flawed.

I was really proud to be among this group of speakers who I found to be "open-access" and very approachable.  I have taken advantage of attending these workshops to ask lots of naive questions to developers, and it is an incredible way to learn and find resources.  Also, notably, I think metagenomics assembly is becoming increasingly relevant to the field as I had more questions than ever after my talk (heh...I know I'm assuming that my talk was clear....)  If any of these subjects interest you, check out the workshop slides.  

### Successful metagenomics analyses integrate iterative approaches
If I had to pick my three favorite talks at the meeting, two of them would be those by Ed Delong and Mary Lidstrom dealing with exploring complex environmental communities with -omic based approaches.  These were great success stories where these two and their teams have made great strides towards understanding environmental interactions.  Quite noticeably, both of these were significant efforts combining a whole suite of tools and integration of environmental -omics (mainly transcriptomics), isolates, labelling methods, and biogeochemical data collection. (I don't think this kind of science is a one-man team anymore given the need for all these approaches.) Ed discussed coupling metabolic activity and gene expression over time in marine communities, published in [Ottensen et al.](http://www.pnas.org/content/early/2013/01/18/1222099110.abstract).  Mary suggested that we redefine the role of methanotrophs in the methane cycle as catalysts and not consumers, published in PeerJ, [Beck et al.](https://peerj.com/articles/23/).  Something that struck me was that they both HAD to use isolates and associated lessons from them to understand their systems.  

The sexiness of environmental -omics often overshadows the critical importance of getting a perspective on cells, populations, and communities before we can understand the ecosystem.  Our available catalog of reference genomes and isolates is increasing (especially for human-related bacteria), and I have been guilty of not leveraging these with my metagenomes.  Reference-based analyses are usually straight-forward and lightning fast computationally.  As easy as it is, there should be a pipeline that just uses it...and lo! and behold! there is for phylogenetic analysis [Metaphlan](http://huttenhower.sph.harvard.edu/metaphlan) and functional explorations should be easy as well so I'm on it!  To clarify, I'm not just talking about sequence comparisons to known proteins but a more in-depth of analysis of the presence of known genomes and the possibility of already having these isolated (if they are important).  

This isn't to say that I think this is the only analysis to be done.  De novo assembly opens up the door for discovery of important proteins that we know nothing about - and that's awesome!  It is still my focus but I'm going to accompany it with some standard reference-based approaches as well.  Anyways, there's the whole other bag of worms that many of our reference annotations are bad quality or wrong...doh.

### Save ancestral strains and label everything 
One of the scariest (yet my fave) talks was given by Tim Barraclough.  He discussed differences in cell growths of ancestral, non-ancestral, monoculture, and polyculture isolates.  And they were all different - even drastically.  Its in his paper by [Lawrence et al.](http://www.plosbiology.org/article/info%3Adoi%2F10.1371%2Fjournal.pbio.1001330) - a great read.  

I've worked with environmental isolates in different degrees during my PhD and postdoc, and I have never thought about saving the ancestral strain or keeping track of the history of a specific isolate.  I could learn a lot from [Rich Lenski](http://myxo.css.msu.edu/) who needs a whole floor of freezers for his E. Coli generations.  The implications that communities adapt to local conditions makes an easy argument for environmental -omic approaches.  

What a quandry...  Environmental studies are so complex that we can't understand them without a reduced system, yet isolate studies arguably don't even come close to ecosystem processes.  Gotta love it.  Some would argue that if we can collect enough data, we'll be able to tease out signals from tons-o -omic data... I'll wait for results from community-supported effort of the [Earth Microbiome Project](http://www.earthmicrobiome.org/).  They'll need some help from some clever bioinformaticians and efficient algorithms soon I bet.
  
It was a great meeting.  I got to see old friends and make new ones and came away with tons of papers to read and more questions than answers.  Since the meeting, I'll admit I'm playing a lot more with QIIME and my shotgun data...and so far so good.  

Happy Friday!  Comments always welcome!
~Adina



 
 

  