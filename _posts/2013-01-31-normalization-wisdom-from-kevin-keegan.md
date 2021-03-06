---
layout: post
title: "Normalization wisdom from Kevin Keegan"
description: "How to normalize metagenomic sequences"
category: 
tags: [metagenomics, normalization]
---
{% include JB/setup %}

Kevin Keegan in our group suggest the following normalization procedure to make samples more comparable (i.e., if one sample had a really good/bad sequencing run to over/under estimate resulting abundances)...

(This is a reflection of what a nice guy Kevin is -- he took the time to write this out for me...)

Through a decade or more of struggling, researches who utilize micro-array data came to a general conclusion that high throughput abundance profiles 
(e.g. expression profiles from microarrays or annotation abundance profiles from generated from high throughput sequence data) should always
undergo a procedure that attempts to reduce global bias and makes samples more comparable to each other.

While a variety of methods have been developed to address this issue, few are in widespread use and are as applicable to different sources of data
than a 2-step procedure that includes normalization and standardization of data within each sample before samples are compared to each other.  Note that these terms are jargon loaded, and are inconsistently used among (and even within) disciplines.  Normalization (as used here) refers to a transformation that attempts to reshape an underlying distribution, from an un-known or non-normal distribution to a normal distribution (think Gaussian or bell curve). A common example in biological data is the application of a log transformation.  A large number of biological variables exhibit a log-normal distribution, meaning that when you transform the data with a log transformation, the values become normal. 

Why do we care about the distribution of the data -- why is a normal distribution desirable?  The quick answer is that parametric statistics (statistics that expect a normal distribution) exhibit greater statistical power (more significance with less data), but can only be applied to data that exhibit a normal distribution.  If your data do not natively possess a normal distribution, it is frequently possible to transform the data into a normal or close to normal distribution.   You should not apply ANOVA or T-test (both are parametric tests) to your data unless you know that the underlying distribution is normal or close to normal.  When data exhibit a non-normal normal or unknown distribution, non-parametric tests (e.g. Man-Whitney or Kurskal-Wallis) should be used.  Scaling values, such that each measure represents x/100% or x/1 IS NOT the same as normalization.

Standardization is a transformation applied to each distribution in a group of distributions (a distribution could be the expression counts from a microarray experiment, or abundance counts from automated annotation of high throughput sequence data with tools like Qiime or MG-RAST) such that all distributions exhibit the same mean (0) and the same standard deviation (1).  In statistical jargon, the location (mean) and scale (~min to max) of each distribution is set to a common value; this renders the data more comparable.  This sort of procedure is analogous to commonly practiced scaling procedures (setting the sum of all expression or abundance values from a sample equal to 100% or 1), but is more robust in that it controls for both scale and location (e.g. setting the sum of abundances to 100% affects scale, but not location).   It is also a more robust procedure than scaling to the value of one or a group of values (e.g. dividing all abundances in a functional profile by the average abundance of several house keeping genes).  The mean and standard deviation of a small group of individual genes is much more liable to stochasticity (background noise) than the mean or standard deviation for all genes on an array or in an annotation abundance profile.  If you use more noise-prone values (e.g. a single abundance value, or average of a small number of abundance values) to scale each individual sample -- the collection of samples will exhibit more noise.   

We suggest a simple procedure to normalize and then standardize abundance count data.  This procedure does two things. First, it attempts to transform the distribution of each dataset to a normal distribution.  Second, it takes the "normalized" values for each dataset and transform them to have the same location(mean of 0) and scale(sd of 1)

First - normalization:
For each value i in a data with abundance from 1 to N, transform each individual value this way

>normalized_value_i = log2(raw_value_i + 1) 

Second - standardize the normalized values
For all abundances from a single sample determine the 
abundance_mean(1 to N)
abundance_standard_deviation(1 to N)
Each standardized value would can be calculated this way:

>standardized_normalized_value_i = (normalized_value_i - abundance_mean) / abundance_standard_deviation

You can read more about these procedures in a number of texts - I'd recommend Terry Speed's "Statistical Analysis of Gene Expression in Microarray Data"

Notes:
Before applying a parametric statistical test - check to make sure that your normalized data actually exhibit a normal distribution.  Boxplots are an easy way to check -- more quantitative tests for normality are also possible (e.g. the d'agostino test ).
If the data don't exhibit a normal distribution (even after normalization), use non parametric tests.
You can also try other methods to normalize the data.

