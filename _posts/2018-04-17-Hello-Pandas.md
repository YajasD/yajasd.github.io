---
layout: post
title: Hello Pandas!
---

## Let's help WTWY

In my endeavor to help a fictitious NGO called WomenTechWomenYes (WTWY), aiming to raise money for their cause through a Spring GALA, organized annually in the month of May - I decided to figure out which locations in NYC would be most suited for their street teams to hand out pamphlets to potential attendees such that they can maximize attendance and donation.

![alt_text](images/IMG_4444.jpg)

## Let's get some data

Best place to get data about humans congregating in specific areas of NYC?
The NYC subway station company.
The Metropolitan Transportation Authority is nice enough to post weekly Turnstile data for all subway stations in New York City.

What's a Turnstile you ask? A Turnstile is the metal barrier you push through to enter/exit a station. Each station has multiple Turnstiles, often grouped together in groups of 2 or more.

![]("turnstile image")

You may find this data here: http://web.mta.info/developers/turnstile.html

## What do your computer eyes see Python?

I find that the number of data points per day remains fairly consistent.

After aggregating certain columns and some addition and subtraction, I'm able to calculate the total number of entries per Turnstile per day. This is an interesting metric.

<paste cells leading up to number of entries column>

<code>

Hmmm....

Let's look at a histogram to get an idea of what the frequency of number of entries looks like.

<Histogram>

Looks like the number of entries per turnstile is around
This is telling me that ~60 million people enter a turnstile everyday. Majority of the data is congregated between 0 and 60 million. It is safe to use that as an upper limit to zoom into the data.
