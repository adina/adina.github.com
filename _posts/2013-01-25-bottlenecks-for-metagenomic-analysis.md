---
layout: post
title: "Bottlenecks for metagenomic analysis"
description: "Recent thoughts from some analyses"
category: 
tags: [metagenomics, analysis, challenges]
---
{% include JB/setup %}


I just came back from a week at Iowa State University with Kirsten
[Hofmockel](http://kirstenhofmockel.org) and her fantastic group.
Team Hofmockel is interested in studying soil microbial communities in
bioenergy crop systems (something I know a little bit about from Jim
[Tiedje](http://www.glbrc.msu.edu) and C. Titus Brown).  We're
combining a nice experiment that involves lots of useful
biogeochemistry measurements with deep metagenomic sequencing (oh
yeah...).  Throw in the support of the DOE [KBase](http://kbase.us)
initiative and my colleagues at ANL, we've got a lot of experts,
tools, and resources in one room. (FYI - these resources are coming
soon to a laboratory near you in late February...I'll blog on it.)

The following is some of the challenges we faced when working with this data:

##  We have a lot of choices from the get-go.

We had 16S amplicons, annotated WGS raw reads, assembled WGS reads, and assembled WGS reads from an alternative assembler.  Do you run the same analysis on all datasets?  Do we look at our annotations at a very fine or broad resolution, i.e., species vs phylum for taxonomy?

## We have "middle numbers" data.

In a recent great [read](http://onlinelibrary.wiley.com/doi/10.1111/j.1365-2664.2006.01188.x/abstract) outlining some key questions and knowledge gaps in ecology, they describe what I agree is a key challenge to using metagenomics to study ecological systems. 

"In small-number systems like the solar system, the relationship between the components, and the state of the system, can often be adequately described by a simple set of equations. In contrast, in large-number systems such as chemical interactions in fluids, the behavior of the system can usually be adequately described using statistical averages because of the large number of components and the simple nature of their interactions.  Ecological systems unfortunately belong to the study of middle numbers; they are too complex to describe individually, yet their components are too few and their interactions too complex to be described by statistical dynamics..."

The "middle" numbers of our soil metagenomes can be attributed to many aspects of our data.  Our sequencing depth only adequately captures a portion (~10%) of the genes in our samples.  Our databases can only annotate ~30% of our data.  I'm confident that metagenomics and scalable approaches can help push us into the "big numbers" with our data.  But does that reduce the complexity?  (Note: if we do not try to reduce the complexity of our datasets, each sample looks randomly different).

##  Reducing the complexity of our data to find signals in our data is... complex.

In the beginning, I think we, and most other people I know, are trying to answer a handful of questions:

1. What is the profile (functional / taxonomic) within a single sample for specific or all functions?

2. Are these profiles different between samples?  

3. How are they different? 

To accomplish this, the first thing that happens is we have to start grouping similar sequences together.  

One way to do this is to annotate the functions of the sequences against known functions and to group them by similarity of function.  This is done so routinely that until the past several weeks I haven't really thought much about it.  It's routine but it's not straight forward.  And I should definitely think about it...I think.

The problems to think about:

### That squirrelly database...

Let's assume I've accepted to move beyond the biases in the database (that's a whole blog on its own)...Its still full of redundant 100% identical sequences with different annotations.  

Examples:
- Conserved sequences between unrelated functions
- Conserved sequences between related functions with slightly different annotations
- Conserved sequences of the same function but from different species
- Conserved sequences with the same function but from different annotation sources

Proposed solution:
- On the database end, some work has been done to try to remove redundancy via the [M5NR](http://press.igsb.anl.gov/mg-rast/howto/m5nr-â-the-m5-non-redundant-protein-database), and I think its a good and necessary effort.  

### BLAST it!...

We say things are similar to a database based usually on some sort of "matched" score.  Often, a sequence can have identical hits to multiple database entries.  In that case, which do we choose?  All the best hits?  A random one?

Proposed solution:
I don't like randomly picking a random best hit.  I think you have to take all the "best"-est hits or you aren't getting a representation of your population.  Can you imagine if the aliens came down and said all of us humans are best hit matches and just selected any one of us to be the single representation for the human race?  Alternately, I guess they could just abduct us all.  Either way...I think we're in trouble.

### Connecting the dots...

There are key connections we like to make about our annotations.  First, we like to group our annotations into even broader groups (i.e., specific metabolic pathways like nitrogen metabolism).  The challenge here is that functions can be involved in multiple groups.  Also, we like to connect our functional annotations with possible taxonomic origins.  Again, multiple functions have multiple taxonomic origins, which then become associated with multiple of the broader functional groups.  These challenges escalate when I think about how you should incorporate the abundance of a sequence which is associated with an annotation, which is associated with multiple organisms and multiple "broader"-functions. 

Proposed solution:
I don't think there is a good solution here.  We're going to have to make assumptions to continue working with the data this.  

Advanced warning:  Get ready for brain explosion!  (Proposed solution: go get a glass of wine)

Let's take an example:  I have a sequence (with abundance of 10) with equal matches to two non-redundant functions.  Non-redundant function #1 is associated with multiple redundant sequences which originate from multiple organisms.  I would argue that you should count each of these organisms as being present 10 times.  Similarly for non-redundant function #2 whose associated sequences originate from multiple organisms -- they should all get a count of 10 too.  If non-redundant functions #1 and #2 are involved in two different broad-function groups, they should also get a count of 10.  And the organism associated with each function would also be associated with the broader-group with a count of 10 (to be combined with other functions in the broad-group).  If non-redundant function #1 and #2 are involved in the same broad-group, it should get a single count of 10 but all the organisms associated with non-redundant #1 and #2 would associated with the broad-function at counts of 10 each.  I've been told that one of the reasons people don't do this is that they don't like it when genus --> class --> phyla --> etc.  don't add up.  I would argue that the comparison shouldn't be done between different taxonomic levels but rather between samples or within a sample (i.e., what is the taxonomic origin of function A vs B?).  My argument for counting everything is similar to my alien argument (officially trademarked heah).  (I should credit Kirsten for pushing me in this direction, so if I'm wrong, I got bad mentorship.  But if I'm right, I'm a brilliant young investigator...with awesome mentorship of course.)

This really bothers me.  It's possible we're overcounting a lot!   How possible is it to determine patterns of correlation when we're doing so much assuming/overestimating?  Our strategy has been to follow original hypotheses related to the experimental design to directly explore specific functions and their originating taxonomy.  Fortunately, we've got other data to provide additional support beyond sequencing data -- someone was a smartie (ISU)!

Anyways, if someone could tell me how to fix this, I'm in.

I can imagine k-mer approaches for unsupervised pattern (no classification, like 16S OTUs) for metagenomes and I think that's where the solution has to lie.  We have some pretty neat ways to think about this in the works with Titus Brown and [khmer](https://github.com/ctb/khmer) software, let's chat if you've got ideas or are interested.
 
## How do you compare different samples (normalization)? 

Most people standardize their datasets by the total # of annotations to make samples more comparable.  

A question that I often wonder is are we transforming real biological signal in our normalization approaches (especially if we don't have replicates to test this).  To fix this, I'm going to push putting spiked standards into all my future metagenomic runs.  I'm not sure what the disadvantage is for this besides some marginal costs.  It would certainly help me out on the analysis end determining how to normalize my data.  We did this with microarrays, no reason not to learn from it, right?

Here's some advice from Kevin [Keegan](http://adina.github.com/2013/01/31/normalization-wisdom-from-kevin-keegan) -- he gave such a nice description that it deserved its own posting!

It'd be awesome if others could share their experiences in challenges/solutions they've had in dealing with metagenomic analysis.  I'm certainly still figuring out how to do this right, and always appreciate advice.

~adina