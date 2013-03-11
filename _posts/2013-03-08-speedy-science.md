---
layout: post
title: "Thoughts on soil metagenomic analysis with IPython and KBase"
description: 
category: 
tags: [kbase, python, collaboration, metagenomics]
---
{% include JB/setup %}

One of my first tasks as a new postdoc at my new gig was to be the "bridge" for a soil metagenomics project between Kirsten [Hofmockel's](http://kirstenhofmockel.org/) "sequencing generation" team at Iowa State University and the "tool development"  [MG-RAST](http://metagenomics.anl.gov/) team at ANL.  Given two months to extract, sequence, and analyze the complex diversity of soil aggregates, my role was to integrate KBase tools and to enable Team Hofmockel to deliver results at the [DOE Grantee's meeting](https://www.orau.gov/gsp2013/default.htm) held in February.

I learned a great deal from this experience and attempt at a summary below.

### Preliminary non-sequencing data, replicates, and aggregates...solid experimental design perks.

A major advantage of the Hofmockel project (and the reason I wanted to be involved)  was its very smart experimental design.  Team Hofmockel is studying the affects of soil aggregates on the microbial community and function in the soil.  One of their goals is to understand the most relevant scale of investigation to study microbes and biogeochemical cycling.  

My experience with bulk and rhizosphere agricultural soil metagenomics has ingrained in me that soil is really really hard!  I keep trying to find simpler systems to study but the importance of understanding soil microbes keeps drawing me in!  And then comes Kirsten's project, trying to break apart (thus hopefully simplifying) relevant pieces of the soil. And to boot, she had already shown with high throughput enzyme activity assays that particular fractions were more "active" with respect to carbon degradation than others.  Woot!  Soil metagenomics and me - together again!

Kirsten's experimental design was to look at aggregate fractions and the complementing whole bulk soil under three land management regimes (prairie, fertilized prairie, and cultivated corn).  As a bonus, she took four replicates of each fraction as well (Y-A-Y for some - though still not enough - statistical power!).  Soil needs very deep sampling (~50 Tbp) to adequately [sample](http://ivory.idyll.org/blog/how-much-sequencing-is-needed.html) it, and so I pushed for deep sequencing of all aggregates of one treatment (deep here is relative = 1 HiSeq flowcell, 3 billions reads), and Kirsten convinced me to throw in sequencing at least one aggregate of multiple treatments.  I figured we could cross-assemble all the sequences from the same treatment together as a reference "combined whole soil" metagenome (leveraging sequencing depth) and tease out the contributions of each fraction (taking advantage of the experimental design replicates).

### Soil aggregates are wicked-diverse and assembly still takes a long time.

I was both disappointed and excited during my assembly efforts to find that there was very little overlap (~10-15%) between sequences from each fraction suggesting high sequence diversity (or an abundance of sequencing error O_o).  

Because folks often ask, I'll report that to assemble all the data we had took about two to three weeks using [diginorm, partitioning, and Velvet](http://arxiv.org/abs/1212.2832).  Assembly of single samples took about half that time.  Surprisingly, it took equally as long to recover the abundance of assembled sequences (by mapping reads back to the assemblies and getting lost in bam/sam files).  

(On a technical sidenote, I used [Bowtie2](http://bowtie-bio.sourceforge.net/bowtie2/manual.shtml) with bam files run with [GNU parallel](http://www.gnu.org/software/parallel/), subsequently parsed with [scripts using PySAM](https://github.com/adina/Dev/blob/master/coverage/sam-to-coverage.py).  If anyone has any suggestions on speeding this up, please shoot me an email.  I think I'll try to switch to k-mer coverage in the future for efficiency.  Anyone who's thinking of doing this, make sure you have mega disk space, I'd suggest at least 5x the size of your data if you're handling assembly and subsequent analysis.)

### Annotations of metagenomes is automated and free but I'm still going to complain.

For metagenomic analysis, I think MG-RAST leads the game in [automated annotations](http://adina.github.com/2012/11/18/the-various-players-in-metagenomic-pipeline-tools/).  They basically absorb all the computation costs and run parallel BLATs on their servers.  My personal feeling on this is that it is not [sustainable](http://xkcd.com/1007/) but as long as its being done, for free, its going to be used and abused.  We ended up running all the raw sequencing reads and multiple assemblies (both single samples and combined field replicates) for annotation.  Hmmm...should we annotate billions of 100 bp reads (see the *abused and free* comment above)?  That's a whole 'nother post but you should all know that [read length matters](http://www.ncbi.nlm.nih.gov/pubmed/18192407) and the time it takes to do this is going to make it impractical in the future. Unsurprisingly, when we were looking into KEGG pathways, we'd find annotations in assembled sequences but none in our unassembled reads annotations.  Its also important to note that our assemblies only represent 10-20% of our sequences...so looking at unassembled data in this case has some merit.

### Collaborative hypothesis testing was fun and easy.

It was a lot of fun working with the Hofmockel team who had lotsa biogeochemistry experience to bring to the table.  And they had hypotheses!  Mainly, we were interested to know if the genetic potential as identified in the metagenomes was supported by the enzyme measurements.  We sequence folk call this stuff metadata, but I think this diminishes the importance of having supporting lines of evidence for observations.  Importantly, this data guided our hypotheses and gave us something to check out within our huge metagenome.

Sidenote:  Like many others, one of the first things we did was to do a statistical analysis of all the annotated functions to see if we could spot anything which looked significantly different in our samples.  I think this grew out of 16S SSU analysis where you get deeper sampling of a single gene.  When I've done this before, and in this case, we see very little differences in our metagenomes.  Basically, we can't see the forests from the trees.  If we had more statistical power and deeper sequencing, I think we could work more with this approach. Presently, I've had much more progress following specific hypotheses (the [debate](http://www.nature.com/nature/journal/v494/n7435/full/494040a.html)).

One of the goals of KBase is to integrate tools like MG-RAST which provide gene annotations and abundances with other types of data (i.e., enzyme data) and statistical packages/languages like R.  Our team consisted of a couple R-aficionados, multiple excel users, and one python programmer.  Given this diversity, anything we wanted to do, someone likely knew how to do it.  The trick was to teach others how to do it as quickly as possible (given our timeline) so that we could divide and conquer to each chase down different hypotheses.  We found iPython notebooks to be an incredible tool to do this in a collaborative environment.  

An example of our workflow would be that I would write up a [notebook](http://nbviewer.ipython.org/urls/raw.github.com/adina/notebooks/master/example-hofmockel.ipynb) which took an input of MG-RAST metagenome IDs (thanks to KBase), pulled out targetted annotations, and compared them across samples.  Kirsten's postdoc would take that same notebook and look at the the same data integrating enzyme measurements.  Kirsten's graduate student would take that data and compare that to 16S SSU amplicons or run statistical tests in R.  We'd all then pass these notebooks amongst each other and rinse and repeat with different enzymes and/or samples (i.e., raw reads vs assemblies).  An example of a real life notebook we used is shown here.  If I shared this with someone else, the only thing that would need to be changed is the specific metagenomes of interest and you could generate new figures for that data with the push of a single button.

This workflow had 3 major advantages for us that allowed us to accomplish analysis very quickly.

- Reproducibly granting access to all domain experts - Anyone on Team Hofmockel could do their own analysis once the notebooks were setup significantly increasing our analysis output.
- Logging - If you wanted to know where any of the figures came from, we had the data and all associated analyses saved in a notebook.  
- Collaborative communication - I could take others scripts and follow the whole workflow without any hidden nuances.  If there were bugs, I could identify them quickly and fix them (usually a little less quickly).

If you're interested in playing with the KBase version of IPython integrated with MG-RAST and R, you can take a look at [KBase Labs](http://kbase.us).  If you're not using KBase, I'd still highly recommend the IPython interface as an awesome way to share analysis between folks with different levels of programming experience.

### Science! - some of our prelim findings...

From this two month push, our data seems to suggest that:

- The community composisiton of field replicates at the aggregate level are similar and can be separated by aggregate size (e.g., small and micro aggregates are different than large macros).
- ~80% of the functions are shared between all aggregates and the whole soil supporting "functional redundancy"
- We observed evidence for niche differentiation between the aggregate communities
- Within the microaggregates, in particular, the abundance of genes encoding for enzymes and their measured activity had the strongest correlations.
- Community related to genes encoding for function were different and could be separated by aggregate size. 

There's lots more to be done yet but this was an exciting start!

## Some challenges and possible solutions

### Expectations and goals of developers vs. scientists were different.

It was a new experience for me to manage both a team of developers and scientists at the same time.  Its not something I would recommend doing as a freshman on a new team with a high priority project that demands being bossy to folks you aren't the official manager of.  

I consider myself more aligned with the scientists using the developed tools than developers.  Perhaps as a consequence of this, I spent much of my time trying to communicate to the developers what the Hofmockel team needed and what "accessibility" meant to us.  Initially, I thought that the developers would create tools that only they could use and others couldn't.  It ended up being the opposite.  The developers wrote demos so easy to use that we could only use them to answer 20% of our questions, and we ended up persistently asking for more and more "raw" data for our analysis.  Its the typical tradeoff between efficiency and flexibility.  The developers were aiming for high efficiency and low flexibility.  We wanted high flexibility and were willing to put in time to develop the efficiency on our own (see Ipython notebook collaboration above). My feeling is that the current form of KBase that I worked with is focused on the former (to involve more of the community) but growing towards the latter as the developers and scientists communicate more (and scientists get increasingly trained).  I'd greedily love to see a model for KBase tools that has users contributing metagenomic analysis or tool integration into a gallery (see [matplotlib](http://matplotlib.org/gallery.html) or [R-gallery](http://gallery.r-enthusiasts.com/)) rather than cookie cutter functions and demos.

### Getting raw data is not as transparently easy as I thought.

One would think that delivering MG-RAST results is the equivalent of attaching an excel file to an email, but I learned that apparently its not.  The KBase environment is built upon users requesting specific data with the equivalent of a web-based query.  Why do it this way?  All the reference databases are in a giant database somewhere in ANL-computer-land that contains your sequence's functional reference hit, its relationship to references in other database, its relationship to hierichical classifications and associated phyla with that function, etc.  This is a lot of information.  To get at this information, you are either going to have to request it specifically and get it delivered to you or download the entire database and the tools to effectively query this database locally.  Currently, things are set up for the former because most people dont have a space or know-how to work with the latter.  This was a severe limitation in our ability to access our data, and we eventually placed a subset of the queried data on a KBase server which was set-up by KBase developers.  Its not practical for this to happen for every user - the developers simply don't have the time or hardware.  It'd be great to see the subset of tools and databases we used installed on an EC2 instance (much like [QIIME](http://qiime.org/install/vm_ec2.html) or [Galaxy](http://wiki.galaxyproject.org/CloudMan/AWS/GettingStarted) implement).  One could imagine then downloading a notebook from the analysis gallery mentioned above and running it locally.  The disadvantage is that you would have to foot the bill for this analysis - but I think this would result in people understanding the real "costs" of efforts like this better.

### Spot check your results.  

Awhile ago I posted a guest blog on normalization recommendations for metagenomic datasets.  The statisticians I know have told me that in order to use certain statistical approaches such as ordination, the data needs to have a normal distribution.  Initially, we did this since its also default in MG-RAST to normalize abundance values.  Looking at our results, we were excited to find some intriguing trends of gene abundance and enzyme activities.  When I went back and looked at the raw data, I found that a lot of the original values were "0".  Huh?  

What had happened is that the "0" values in each dataset were transformed into non-zero values during normalization.  Additionally, this transformation would result in different values for each dataset.  Thus, abundances which were initially similarly "0" in our different samples were now possibly significantly different when transformed.  Wrong!  After kicking myself a bunch of times, I went back and thought about our goals.  We wanted to identify the abundance of Gene X and compare this abundance among different samples.  Since each sample had varying numbers of reads, we needed to standardize our abundances by some consistent measure in all samples.  One could argue what this unit of measure should be -- total number of reads, total number of annotated reads, total number of cells, etc.  

We decided on standardizing by the total number of single-copy housekeeping genes in each samples (an idea Tracy Teal has used in her metagenomic analysis very effectively).  We checked that once you normalize by a select housekeeping gene,(we used rpoB) that you'd get similar values for other housekeeping genes (i.e., gyrB, recA) if you account for gene length.  This works out well because once you divide by the total number of rpoBs, you get an abundance that is interpretable as a "per cell" equivalent.  It made sense to say that there were 0.3 chitinase genes identified per cell in the community.  That's more interpretable than saying there are 3 chitinase genes per 100,000 sequencing reads to most ecologists I know.  

So lesson learned...we don't recommend normalizing the datasets but rather standardizing by number of housekeeping genes.  I think there is a whole lot of room for developing better statistics for analyzing metagenomic datasets which are not normal in distribution - Bayesian statisticians are welcome to pipe in here.  

A take home from this lesson for me is that you should try to understand all aspects of your analysis, and if you can't, be wary.  I blindly followed an approach which might be more appropriate for other analysis and thus needed to course correct.  Luckily, because we'd logged our analyses in the notebooks, we could repeat them easily with different inputs.

### Conclusions 

All in all, working on this timeline was really stressful and not something I want to do in the very near future but it forced me and Team Hofmockel to commit to trying things outside our comfort zone.  It ends up that this strategy works well for me, and I feel well-prepped to take on the next steps of this analysis with their team.  There's nothing like a committed and enthusiastic team to get science done, and I'm looking forward to more of it soon!  I think KBase enabled some neat integration of tools which has great potential, and there is a real need for users to engage and contribute to its future development to ensure the most useful product.       

Comments always welcome!

-adina








 
