---
layout: post
title: "Lightning Network Cohort Analysis: Data"
categories: Lightning
author:
- sorukumar
---

 - How many new nodes sign up each month
 - How many we loose per month
 - How do nodes behave when they sign-up, How long they are alive before they are dead. Do they come alive from dead? Do they resurrect?

These questions come to mind when we start thinking about growth of Lightning network. 

The goal of this post is to share data, and provide some interpretation. In the next iteration of cohort analysis, I'll pass more coherent and holistic story.


## The Data & the Methodology

**Data:**
We have LN graph output from an LND node since May-2023. We are analysing graph data pulled on a day of the first week for following months. Here is how the data looks.

![# of LN Node]({{ 'assets/CohortNode.png' | relative_url }})

#of Nodes is count of unique pub key from the graph output. 
Active nodes: Nodes with at least one active public channel that has sent at least one update to its peer.

What you need to make a note, looking at the table above:

 - There is no data for June, July and September. It just tells you I was not looking to store historical data for analysis at that time. Nonetheless, for our puspose, 9 months of data is enough
 - We'll focus our analysis on only active nodes.

**Methodology:**

 - We'll look at all active nodes in a month, and continue monitoring how many of 	them are active in subsequent months
 -  We'll also monitor how many 'new and resurrected' node we see in a month, and we'll also follow their behavior in analysis window.
 - New and resurrected nodes for a month are nodes we are seeing for the first time in the observation window ( October-23  to April-24) . For December cohort,  the # of new and resurrected nodes are nodes that we saw first time in December in our observation window, that is we didnt see them in October or November.
 - Why not just new, why 'new and resurrected'? They could be a resurrected node as well. For example, a node that was active in August, but not active in October, november and again start showing up in December is getting counted in December Cohort. What % of these nodes are resurrected? Based on additional data I estimate that ~30% of those nodes could be resurrected. We'll do a thourogh analysis in the next iteration.

## Heat Map

![Cohort Heatmap ]({{ 'assets/Cohortheatmapoctv0.png' | relative_url }})

What to read from the heatmap above:

 1. Row 1, out of ~10K nodes active in october, 90% would stay active for next 3 months, but after 6 months, only 75% would stay active. I have seen from additional months of data that the trend holds.
 2. From row 2-7, ~60% of new and resurrected nodes stay active after 4-5 months.
 3. I'm pleased if you are wondering why the # for  'new and resurrected node' is trending down, from 416 in Nov-23 to 284 in Apr24. A newer version of the heatmap above will make it easier to understand.

![Cohort Heatmap ]({{ 'assets/CohortHeatmapOct.png' | relative_url }})

## How many we loose each month

All your files and folders are presented as a tree in the file explorer. You can switch from one to another by clicking a file in the tree.

## Cohort of Currently Active nodes

You can rename the current file by clicking the file name in the navigation bar or by clicking the **Rename** button in the file explorer.

## Nodes behavor based on when they have signed-up



## Notes

In general, LN is still an early technology, so a lot of nodes are just Ln enthusiast playing around, and a lot of big nodes are bitcoin business who are here to support the technology  and reap the benefit of being an early adopter. So, in short, dont read too much on data as the behavior will keep changing as the ride along the adoption curve.




<!--stackedit_data:
eyJoaXN0b3J5IjpbNjQyNjEyNjczLC0xNTE1MTQyODgwLDc0Nz
Y1NjIwMiwtODgzMTk1MzIsLTExOTU2MDcwNTIsMzg0NzQ5Nzc0
XX0=
-->