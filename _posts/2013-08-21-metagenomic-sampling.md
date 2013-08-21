---
layout: post
title: "Metagenomic Comparisons of Different Sampling"
description: "How to compare datasets of different sizes?"
category: 
tags: [metagenomics, normalization]
---
{% include JB/setup %}

I've been working on comparing multiple soil metagenomes and am revisiting the topic of how to compare datasets with large variations in the number of reads (e.g., sampling depth). I think its an important and often overlooked topic in metagenomic comparisons. 

I've previously struggled with this topic, and you can see some posts on [here](http://adina.github.io/2013/01/25/bottlenecks-for-metagenomic-analysis/) and a guest post which I've decided I don't generally agree with [here](http://adina.github.io/2013/01/31/normalization-wisdom-from-kevin-keegan/). 

### The Problem - Different sampling depths

If you generate 20 different metagenomes from the same soil plot, I can guarantee that they will differ in the number of reads each will yield.  When we did this, I had samples yielding from 15 to 290 million reads (with a pretty even spread in between).  That's a wild range!  You might be asking why I didn't have my sequencing core re-run my lower yield samples...in 20/20 hindsight, I wish I had for a few samples.  But at the time, I was really excited to get my data (and under a production timecrunch).  I have a general attitude that sequencing is going to be wacky no matter what - so I rolled with it.  

The question then is:  how do you compare a 15 million read dataset to a 290 million read dataset?  

There are pretty much two approaches -- and both have been applied to targeted 16S rRNA sequence analysis. First, you could "subsample" your larger dataset to make uniform numbers of cells (reads) for all the samples.  Second, you can normalize each dataset by dividing by the total number of cells.  Note that in 16S, the number of cells is assumed to be equal to the number of reads.  For WGS data, you could use a number of single copy genes.  I use recA based on previous research I've done showing that it is the best estimate for [a simulated metagenome](http://adina.github.io/2012/11/07/the-importance-of-control/).

### How many cells are in the two datasets?

To put this in perspective, let me tell you about how many cells I think I'm sampling in a metagenome:

![Figure 1](https://raw.github.com/adina/adina.github.com/master/_site/figures/reca.png)

In 2 million reads, there are rougly 15 recA genes in my metagenome assembly (note assembly here, not raw reads) and in 200 million reads, this increases linearly to roughly 1000 recA genes (e.g., cells).  This number is really useful to know but its also a bit sobering.  One lane of a HiSeq (200-250 mill reads) will only assemble the phylogenetic marker of roughly 1000 cells and many of them might be the same.  Let's not complain though, we gotta start somewhere -- last I did a real count (a few years ago), there were less than 1000 soil genomes available.

I performed a similar analysis to determine how many "functions" I could identify with increasing read volumes and found a similar linear trend.  I was able to identify roughly 4300 copies of functions (carbon-cycling related) with 1 million reads and 100,000 copies with 100 million reads.  In general, this linear growth was good to see.  To me, it meant that if we sequence more reads, I could predictably tell you how much more we could identify.

Digression on methods here:  To get these numbers I performed multiple (n=100) random samplings of the largest dataset I had -- and this is actually a giant pain in the butt for assembly (e.g. versus rarefaction/subsampling of 16S data or unassembled reads) -- can you figure out why?  Its another blogpost in the future.

### Does linear abundance growth with increased sampling equate to the same diversity profile?
We know that we see a linear increase in abundance with increasing numbers of sequencing reads but does do our functional profiles change also?  In other words, are we sure we see the same things but in different proportions in the 15 million vs. 290 million read dataset?    

Here's a couple different perspectives that show that things don't change much past about 10 million total reads (5e6 paired reads in figures):

This shows the profile of different functional classes with increasing number of reads.

![Figure 2](https://raw.github.com/adina/adina.github.com/master/figures/2013-08-21/barstacked.png)

This shows the number of unique functional classes with increasing number of reads.
![Figure 3](https://raw.github.com/adina/adina.github.com/master/figures/2013-08-21/function.png)

Ok then! I'd conclude here that 15 million and 290 million datasets are comparable (if normalized to number total number of cells).

### What is actually changing?

Hmmm...this data indicates that I only need about 10 million reads, and I've got what I need.  (I'm totally ignored the ton of preceeding work I put in that DID require many more reads, e.g., assembly).  I'm going to bring up another topic of fun debate and that is "species definition" and what is the most appropriate "bin" to informatively classify sequences into.  For example, if I were to classify sequences into their phylogenetic domains, we'd only have three bins (archaea, bacteria, and eukarya) unless you're wanting a fight and then you'd choose something less Woese-ian (like prokaryotes and eukaryotes).  Alternately, you could also cluster sequences into something like an operational functional unit (similar to a 16S OTU) where sequences share 10% identity (arbitrarily).  Doing so, you'd have many more bins and increased resolution of differentiating your samples.  I did this with the same sequencing dataset below - it represents a more strict bining of sequences to specific sequences.

More conservating binning to measure a "unique function":
![Figure 3](https://raw.github.com/adina/adina.github.com/master/figures/2013-08-21/contigs_bin.png)

Here, you can see that we see a significantly different saturation point, suggesting needing more like 100 million paired reads to adequately sample at this resolution.  

### What is right?

The short answer is that It Depends.  If you don't know how to answer any difficult question, there are two go to answers.  The first is "the situation is complex".  I use this one in any political discussions at the in-laws.  The other is almost always correct when talking about sequencing, "It depends on your question."  

Soil is a fun (but challenging) place to work right now.  We know SO VERY LITTLE that almost any insight in understanding its complexity should be shared. 

In conclusion, I feel pretty comfortable keeping the resolution of my study fairly "low" here.  Hopefully, I've convinced you that it is okay to compare a small and large dataset based on the above analyses.  For my questions, I'll normalize by the number of cells (or the number of recA genes) and I think we'll be good to go.  But obviously, there are improved resolutions that may be increasingly important in the future as we figure out more.  I also want to point out that improved resolutions here depends on getting more references, which we are in desperate need of in the soil.  

### A useful analogy
A good analogy I often turn to when thinking of sampling is to think of sequencing depths as photo snapshots at different resolutions.  You can think of a pixel as a read.  Some of my "photos" have pretty bad resolution, only a few pixels.  Some are in high definition - where you can see even TOO much.  Do you dial back the resolution on all photos to see if they are the same?  If you dial back too much, you wont be able to tell what you're looking at.  There is a sweet spot you can dial back to where things look the same (broadly speaking).  If you have a very specific interest, you might want to just look at the high resolution photo first and then look for those signals in the other photos.  What you really want though is to have the OPTION to adjust the dial.  That's where everyone wins.

~Adina



 

