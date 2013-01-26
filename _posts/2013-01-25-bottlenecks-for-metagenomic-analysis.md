---
layout: post
title: "Bottlenecks for metagenomic analysis"
description: "Recent thoughts from some analyses"
category: 
tags: [metagenomics, analysis, challenges]
---
{% include JB/setup %}

I just came back from a week at Iowa State University with Kirsten Hofmockel and her fantastic group.  Team Hofmockel is interested in studying soil microbial communities in bioenergy crop systems (something I know a little bit about from Jim Tiedje and C. Titus Brown).  We're combining a nice experiment  that involves lots of useful biogeochemistry measurements with deep metagenomic sequencing (oh yeah...).  Throw in the support of the DOE KBase initiative and my colleagues at ANL, we've got a lot of experts, tools, and resources in one room. #KBase Link>  (FYI - these resources are coming soon to a laboratory near you in late February...I'll blog on it.)

The following is some of the challenges we faced when working with this data:

##  We have a lot of choices from the get-go.

We had 16S amplicons, annotated WGS raw reads, assembled WGS reads, and assembled WGS reads from an alternative assembler.  Do you run the same analysis on all datasets?  Do we look at our annotations at a very fine or broad resolution, i.e., species vs phylum for taxonomy?

## We have "middle numbers" data.

In a recent great read outlining some key questions and knowledge gaps in ecology, they describe what I agree is a key challenge to using metagenomics to study ecological systems. #link to 100?s paper#

"In small-number systems like the solar system, the relationship between the components, and the state of the system, can often be adequately described by a simple set of equations. In contrast, in large-number systems such as chemical interactions in fluids, the behavior of the system can usually be adequately described using statistical averages because of the large number of components and the simple nature of their interactions.  Ecological systems unfortunately belong to the study of middle numbers; they are too complex to describe individually, yet their components are too few and their interactions too complex to be described by statistical dynamics..."

The "middle" numbers of our soil metagenomes can be attributed to many aspects of our data.  Our sequencing depth only adequately captures a portion (~10%) of the genes in our samples.  Our databases can only annotate ~30% of our data.  I'm confident that metagenomics and scalable approaches can help push us into the "big numbers" with our data.  But does that reduce the complexity?  (Note: if we do not try to reduce the complexity of our datasets, each sample looks randomly different).

##  Reducing the complexity of our data to find signals in our data is... complex.

We primarily took one approach to simplify our datasets, we tried to group similar sequences together.  For example, exploring function, we might cluster all genes related to DNA replication or Nitrogen metabolism together. #seed subsystems#  Alternately, we might perform an ordination of all classes of taxa and extract significant groupings from statistical analysis. #vegan citation#  In my mind, this is similar to supervised (classification) or unsupervised grouping (ordination methods).  One could also combine these, i.e., ordination of classified groupings.  (Note: Again, a lot of choices and analyses to perform...the value of replication of analysis is high here.)

Let's take a step back and think about what goes into classification and annotating a sequence.  

Like many others, we annotated biological features based on sequence similarity to a database.  This database of who's and what's could and does contain:

1. A unique sequence of a single function that has only been seen once in a single genus
2. Multiple sequences (100% identical) of a single function which originate from multiple organisms
3. Multiple sequences of multiple functions which originate from multiple organisms

For practical purposes, let's call each of these database entries an "annotation node".  As we group related annotation nodes, things get a dicey and we're going to make some decisions.  

Group 1:

Annotation Node #1 - Type III, enzyme 1, enzyme 2, genus 1, genus 2 - abundance = 5

Annotation Node #2 - Type III, enzyme 3, enzyme 4, genus 3, genus 4 - abundance = 3

Now we have two groups of higher level functions that are related to multiple functions and organisms.  The question is what is the abundance and functions related to the two groups and how do you attribute counts of abundance to each item within an annotation node?  Does each item get the same count?  A relative fraction of the count?  Do you pick a representative (randomly, LCA, etc?)  Thinking on this, I think it depends on your question.  If I want to compare the presence of functions related in Group 1 between two samples, it would be reasonable to only count a single representative of each annotation node (i.e., enzyme 1 and enzyme 3).  And then the associated phyla (genuses 1 and 3) corresponding to that function would only be represented, excluding  genuses 2 and 3.  Alternately, if I wanted to know the group of bacteria that could potentially contribute to providing group 2 functions (and then compare this between metagenomes), I would want to include all information in each annotation node.  

The ability to flexibly choose these annotations and return this data to the users has been both a goal and challenge to our group.  I'm still not sure which to tell users is correct.  

## How do you compare different samples (normalization)? 

Most people standardize their datasets by the total # of annotations to make samples more comparable.  Kevin Keegan in our group suggest the following normalization procedure to make samples more comparable (i.e., if one sample had a really good/bad sequencing run to over/under estimate resulting abundances):


A question that I often wonder is are we transforming real biological signal in our normalization approaches (especially if we don't have replicates to test this).  To fix this, I'm going to push putting spiked standards into all my future metagenomic runs.  I'm not sure what the disadvantage is for this besides some marginal costs.  It would certainly help me out on the analysis end determining how to normalize my data.  We did this with microarrays, no reason not to learn from it, right?

Concluding, my advice to our team is to follow their original hypotheses with very directed tests, i.e., select specific functions they expect to be the same  or different in metagenomes.  Fortunately, they've got other data to help provide support for evidence in metagenomes -- aren't they smart!

I'd be delighted if others could share their experiences in challenges/solutions they've had in dealing with metagenomic analysis.  I'm certainly still figuring out how to do this right, and always appreciate advice.

~adina
