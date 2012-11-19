---
layout: post
title: "Quickie on Metagenomic Analysis Tools"
description: "My two-cents from using the metagenomic annotation tools"
category: 
tags: [pipelines, annotation, bioinformatics]
---
{% include JB/setup %}

About a year ago, I was sitting on a 3 billion read soil metagenome trying to figure out how to take it from data to information, or sequencing to function.  I needed some annotations!  So, the not-so-brilliant bioinformatician I was, I decided to take a subset of my data, break it up into a thousand chunks, and run a BLAST and even a BLAT (because I heard this was faster) on it.  Luckily, I figured that this would take another 50 years before it would finish, even for a subset.  Jared Wilkening does a nice write up on computational costs of this [here](https://www.mcs.anl.gov/uploads/cels/papers/P1665A.pdf).  

Given my failure to annotate things with my fairly extensive computational resources and access to decent computational biologists, I had a couple of choices.  I could make this someone else's problem -- there are several automated metagenome pipelines. However, I like to consider myself a "responsible scientist" and not do things that would-take-forever-to-upload-on-a-webserver or not-recommended-for-really-short-reads.  

At the time, we were working on assembly, and I just put all my eggs in one basket and hoped we'd figure out a better way to get the data reduced to a manageable state -- and we did.  See Titus's [post](http://ivory.idyll.org/blog/an-assembly-handbook-for-khmer.html), the paper is coming out soon as well.

In the end, I threw about 30 million soil reads at CAMERA, IMG/M, and MG-RAST.  I wanted to know what was in there!  In working with these tools, I became familiar with what the key steps to metagenomic analysis include:

1) Data upload - pray that you get an FTP option for your HiSeq sequences

2) Metadata upload 

3) Quality Filtering/Dereplication - Error reduction

4) Identification of Protein Coding Sequence - Gene Calling of Protein Coding Regions (Noncoding is left behind here)

5) Clustering / Dereplication - Eliminate Redundancies

6) Annotation against known databases

Note that steps #3, #4, and #5 focus on reducing the amount of data for the computationally expensive step #6. (I'd suggest trying assembly for orders of magnitude reduction).

The three pipelines do each of these steps in slightly different ways.  Mainly, they each select specific tools and databases your data goes through.  There seems to be two camps for the "automatic pipline" developers.  The first allows users to be highly flexible in the choice of tools and parameters, chosen in each step.  The second takes the data from start to finish, asking few to no questions in between. I personally much prefer the first way of doing things, but I have years of experience to build from in making these choices.  That simply isn't true by researchers confronted with mega-sequencing data nowadays.  

In pipeline camp 1, CAMERA lives very comfortably.  In camp 2, with a beginning to end analysis, IMG/M and MG-RAST share the real estate.  MG-RAST (since I'm here now and am in-the-know) is moving towards increasing user flexibility, developing a way to provide an R-integrated analysis package, etc., but this is still in development.  They are always looking for beta-testers (https://github.com/MG-RAST/matR).

I know inexperienced users, like my past self, will take the easy way out with these pipelines.  Why not just upload my billions of reads right on in for annotation?  Sure, calling a gene coding region AND finding solid annotation hit may be sketchy, but I get an annotation, right?  Oh yeah, and these annotations, I'll make them public and then someone else can proliferate my not-so-accurate annotation.  As you can see, I'm not a big fan of uploading short reads to these pipelines!

Many microbiologists do not think of data analysis as an experimental step (let alone multiple steps). How can we as developers convince users to think critically about analysis being an experimental step while providing ease-of-use tools?

Comments welcome!









 


