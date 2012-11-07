---
layout: post
title: "The Importance of Control"
description: ""
category: 
tags: []
---
{% include JB/setup %}

# The Importance of Control

Recently, I've been spending a lot of time combining overlapping short sequencing reads (100 bp) into longer sequences called contigs.  Since I'm doing this without any reference genomes, this is called de novo assembly.  (Here's a really nice introduction into the subject from the University of Maryland, [Primer](http://www.cbcb.umd.edu/research/assembly_primer.shtml).

The datasets I'm working with are challenging in a couple unique ways.  Firstly, they're ginormous, 3 billion reads (300 billion bp or the equivalent of 75,000 E. coli genomes).  This has been the subject of many of my pal and previous boss, C. Titus Brown's blogposts, [Living in an Ivory Basement](http://ivory.idyll.org/blog/)).  We think we have a good grasp on how to process and assemble this data nowadays.   One of the key things I realized while dealing with this first challenge was the second problem...and that is, how do we know what we're getting out is right?  Are the assemblies we produce correct?   Basically, are the methods we are using doing what I think they are? 

The idea of a "unit test" has been one that I have been learning a lot about as I am starting to both produce and teach more scientific coding.  For those who are starting out in this field, I've basically infiltrated after three years -- its doable and very rewarding.  Looking back to my time as an experimental microbiologist, this is very analogous to the requirement of controls for an experiment in that one would ALWAYS require.  In bioinformatics, I have adjusted my perspective to crave the same reassurance.

In choosing such "controls" for metagenomic datasets, many others have chosen simulated metagenomes (mixtures of reference genomes with some error profiles mixed in).  I think these datasets are useful but the problem is that it does not reflect real data.  We've seen systematic biases in metagenomic datasets which due to their seemingly random nature cannot be captured in a simulated error profile.  

Fortunately, the folks at the NIH Human Microbiome Project have made a push for protocol development and validation.  This has resulted in an immensely useful "control" mock genome for me.  This dataset is the sequencing of an experimental mixture of DNA extracted from isolates.  (There are actually two datasets, an even and staggered mixture).  Although this mock genome is NOT a metagenome, it has two properties that are wonderful:  first, it has the dirty noisy characteristics of a real metagenome since it has actually gone through the sequencing process and secondly, it has a set of references with which to examine any analysis. 

I want to highlight a couple use cases where I have found this dataset (or something like it) to be critical.  

###\#1 Evaluation of Digital Normalization and Partitioning for Assembly

Briefly, our approaches efficiently sift through metagenomic data and eliminate redundant information above a user-defined threshold (i.e., you only need to see an overlap X number of times before you're sure that it should be assembled).  We then break apart pieces of the total metagenome which are not connected (i.e. separating genome A and B).  We then assemble each of these "partitions" independently.  I needed to evaluate what was happening when we're discarding data and manipulating data in different groups.  Using the mock dataset, I assembled the unprocessed dataset with a variety of assemblers and compared this to the processed dataset assembled.  I could determine the similarity between assemblies and most importantly, the recovery of reference genomes.  Awesomely, I found that after I processed the mock metagenome, I got better assemblies!


![Table 1](https://raw.github.com/adina/adina.github.com/master/_posts/figures/2012-11-06-control/table1.png)


Table 1. Assembly comparisons of unfiltered (UF) and filtered (F) or filtered/partitioned (FP) HMP mock datasets using different assemblers (Velvet (V), MetaIDBA (M) and SOAPdenovo (S)).  Assembly content similarity is based on the fraction of alignment of assemblies and similarly, the coverage of reference genomes is based on the alignment of assembled contigs to reference genomes (RG).

###\#2 Identifying Housekeeping Genes in Assembled Contigs

I had a problem in that I needed to determine how to compare different metagenomic assemblies of two different samples.  I decided I would normalize by some known housekeeping genes as a proxy for number of genomes.  The problem is that I wasn't sure how accurate a reference based annotation (using HMMER) of various gene models (recA, rpoB, gyrB, etc.) against my assembled contigs would fair.  Using the mock metagenome (containing 21 genomes), I was able to determine that estimates of the mock community there were some gene models, gyrB and rpoB, (because of their length) were not candidates. These would overestimate the total number of genomes.

![Table 2](https://raw.github.com/adina/adina.github.com/master/_posts/figures/2012-11-06-control/table2.png)

Table 2. Number of housekeeping genes identified in HMP mock community reference genomes and assembled (Velvet) contigs.

If I've convinced you that you'd like to control everything in your life too, you probably want to know where you can get this data?  It's a bit hard to find.  Google would most likely bring you the following description of lots of datasets you could play with (mostly dealing with 16S amplicon sequencing): 

> <http://hmpdacc.org/doc/HMP_Data_Set_Documentation.pdf>

I couldn't get the download links to work and cannot find the described 4 sequencing datasets for a mock community.  What I can help you with is a link (thanks to Mihai Pop) to the SRA Illumina mock genomes:

> Staggered

> <http://www.ncbi.nlm.nih.gov/sra/SRX055381>

> Even


> <http://www.ncbi.nlm.nih.gov/sra/SRX055380>

> Reference Genomes

> [FTP for reference genomes](ftp://ftp.hgsc.bcm.tmc.edu/pub/misc/HMP/mock/mock.all.genome.fa)

Some information on relative abundance of each genome in the mixture can be found here (thanks to Stephen Turner!)

> <http://downloads.hmpdacc.org/data/HMMC/HMPRP_sT1-Mock.pdf>

Though I caution you that I do not find these abundances to be accurate based on my assembly of this dataset.

Also, in case you don't know how to work with the SRA or get stuck in what is the perpetual link-loop purgatory within the SRA (as I often do), I've also placed them here:

> [Even HMP mock fastq]("http://lyorn.idyll.org/~adina/SRR172902.fastq.gz")


> [Staggered HMP mock fastq]("http://lyorn.idyll.org/~adina/SRR172903.fastq.gz")

I hope you enjoy control as much as I do.

Signing off my very first blog post (woot!),

Adina
