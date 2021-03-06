---
layout: post
title: "Thoughts from the EPA Air Sensors Workshop (Big Data)"
description: "Insight into my relationship defining talk with Big Data"
category: 
tags: [big data]
---
{% include JB/setup %}

I've just returned from the [EPA Air Sensors Workshop](https://sites.google.com/site/airsensors2013/home) in sunny and warm Raleigh, NC (grrr...Michigan winter).  I was invited out as a suggestion by my previous boss, a [sequencing big-data guru](http://ged.msu.edu/).  Some folks at the EPA community had heard [his talk at the National Academy of Sciences](http://www.slideshare.net/c.titus.brown/2013-nasehsdataintegrationdc) and invited him out, but they got me instead.  Bwahahahahah.  

## My relationship defining talk with Big Data 

Initially, I was more than a little tenuous about my ability to deliver a big data talk.  Reflecting back, per the norm, I was being silly. What defines a big data expert after all?  I've been in a role somewhere between data generator, tool developer, and data integrator/analyzer for large sequencing datasets for years now.  Having these varying experiences has given me different perspectives of big data problems in different domains.  At this meeting, I was given a neat opportunity to communicate (hopefully helpfully) what a big data deluge feels like to folks in these different roles, and what the specific challenges and solutions might be.  

At the meeting, I gave a [15 minute presentation](http://www.slideshare.net/adinachuanghowe/epa-mar2013-bigdata) on big data in biology, but the real fun was talking to folks after my talk and at the subsequent breakout sessions.  It was a novel experience to be communicating about "lessons learned" to people outside my field who are actually anticipating and preparing for all the problems I found myself immersed in.  It was also fun to be representing an entire field, encouraging me to not be as shy as I typically may have been.  

## Meeting Highlights

I'll tried to summarize some points that stuck with me from my conversations in either breakout groups or with individuals.

###The flavor of the crowd

Many of the folks I talked to wanted some sort of platform to start integrating different types of datasets.  At least two people independently mentioned a specific example of integrating Google traffic data, air quality data, and some sort of human health indicator (i.e., asthma reactions).  

Others pointed out that they wanted the "Google" equivalent to search sensor data.  It was pointed out to me that such a [site does exist](http://www.data.gov), but the consensus was that people didn't like it that much (a well-intentioned unused tool by this community at least).  Digging deeper, the main reason for this was that they either couldn't find the right data or couldn't figure out how to "integrate" (also known as "mashup") different types of data.  

My feeling was that folks wanted more than a "search function" -- they wanted a platform with multiple functions (extending from a google search-like service to integration and analysis services). 

###Standards always get a priority in the discussion.
Typical to biological equivalents of similar conversations, discussions often moved towards the need for standards of metadata accompanying datasets.  Standards and I have a love-hate relationship -- see this clever [XKCD](http://xkcd.com/927/
) for explanation.  The need for a good quality and quantity of metadata is obvious in its usefulness to me.  I'm just not sure how to get this done in an environment where everyone has different goals in a data collecting community.  The flexibility of data access accompanies "loose" standardization.  I did note that the existence of some sort of standard helps me figure out what kind of data I should collect when sampling though -- a +1 for standards I often forget about.

On a related side note about metagenomic standards:  MG-RAST (metagenomic annotation pipeline and data repository) has adopted the [Genome Standards Consortium's template](http://gensc.org/gc_wiki/index.php/MIGS/MIMS) for metadata standards for metagenomic data. I just had a conversation with our team that I didn't think that most people didn't put in metadata because they didn't want to share it but rather because it was nearly impossible to put into our [current format](http://press.igsb.anl.gov/mgrdev/learning-mg-rast/metadata-in-mg-rast/).  Its possible that we've been operating on a "nobody wants to share" assumption when the implementation of how to put in standards might be at fault. (We're going to start some logging and find out though -- I'll report on this in the future.)  

###Thinking about levels of function (not data)
Many folks agreed that they had to deal with different types of data and suggested that there should be different levels of organization of this data in a big data solution.  An interesting example and model of unqualified data integration is [Weather Underground](http://www.wunderground.com/) which collects weather-related measurements from anyone with a sensor who wants to contribute.  When using Weather Underground data, one might want to integrate "citizen-collected" datasets differently than EPA collected data.  Flipped around, you might want to provide different sorts of data output to the public than you might to researchers.  (Sidenote:  its nifty how much community involvement in data collection there was here -- something we're only [starting to think about in our field](http://www.indiegogo.com/projects/ubiome-sequencing-your-microbiome?website_name=ubiome).

I tried to point out that the *growing* diversity of the types of questions, datasets, users, and tools is limited by structuring data access to "data types" (i.e. citizen science data vs. EPA sensor data).  After all, not all data queries need data to be separated by who collected that data nor will all data have that sort of metadata available.  To provide the most use of datasets, I suggested you have to provide high flexibility in the access to the data through different *services*.  For example, a particular service could take all weather sensor data and separate data by its origin (i.e.,  citizens vs. the EPA).  Another service could give you the average  of all weather data collected during a particular week.  Another service could integrate these two services to give you the average weather data separated by who provided that data.  And you could pretty easily exploit the same services for other data types -- i.e., exploring air quality data (analogous to weather data) and the brands of sensor used (analogous to user-origin metadata). 

I gave examples of the [KBase infrastructure](www.kbase.us) where we try to build off a low-level data store and general data query services in layers of increasingly higher level functions.  I suggested that we imagine all the data in one place where we could access it. And then identify what kind of analysis/services we wanted to perform an this data?  What's the data analysis end game and how could we get there?  And then for people with different end games, I asked if they thought they could share the same resources of someone else's effort.  It was fun to think about what this would look like for sensor data, and it gave me a better understanding of why I think the KBase model is a good one.  

Interestingly, a handful of attendees (and this is may be something political that I don't understand) were interested in "data widgets" rather than whole platforms.  I had a really hard time communicating that the widgets that they wanted could part of a platform solution.  I can only assume that a "widget" is something they could buy independently vs. a platform which would be a community-driven investment.  

###Not-as-big data at high velocity

Air sensor data can be measured in seconds and needs to be analyzed and communicated in very short periods of time -- think summaries of [daily air quality](http://airnow.gov/).  I started mulling about what this means for data management and integration.  The focus here is on arguably less heterogeneous datasets (compared to biological data) but the ability to process and integrate it rapidly.  A solution here would be to have a service that takes care of streaming and automating data delivery, analysis, and communication connected to platform that might just store the data so that it could be integrated with other services.  This form of rapid exploration of data doesn't exist in the sequencing framework right now because the sequencers take too long to provide data and the subsequent analysis takes even longer.  

I started to think about what our field and data would look like if we could do this - access real time sequencing data.  As a fun walk in daydreaming mode, I imagined getting streaming sequencing data for a transcriptome expressed in "real time" and being able to provide live assessment of the regulation processes that were changing or not changing.  This could be a happy chemostat of a bacterial community with robots doing DNA extraction and library prep going right into a sequencer and a spiffy computer doing online, [streaming analysis](http://ged.msu.edu/papers/2012-diginorm/) identifying differential expression.  Often sequencing folks get real excited about long reads (which unless its complemented by deep sampling isn't a solution for high diversity samples).  Thinking of sequencing as "real time sensors" got me excited about rapid exploration -- which big data management and computational efficiency is definitely a part of the solution.  +1 for continuing my work.

Overall, it was a great experience at the workshop.  People were super friendly, enthusiastic, and did a great job making me feel useful (even to the point of blowing up my ego.)  I'm really glad I got invited and convinced to go. If you get a chance to have an out-of-domain-expertise experience, do it!

Love to hear your feedback always!

~Adina     
