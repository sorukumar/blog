
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


## The data & Methodology

**data:**
We have LN graph output from an LND node since May-2023. We are analysing graph data pulled on a day of the first week for following months. Here is how the data looks.


![# of LN Node]({{ 'assets/CohortNode.png' | relative_url }})


#of Nodes is count of unique pub key from the graph output. But depending on who we want to count as nodes, lets define active node as well.
Active nodes: Nodes with at least one active public channel that has sent at least one update.

Please note that:

 - I dont have data for June, July and September. So, for our puspose, we'll analyze 9 months of data to understand cohort behavior
 - We'll focus our analysis on only active nodes.

**Methodology:** 
	 - We'll look at all active nodes in a month, and continue monitoring how many of 	them are active in subsequent months
	 - We'll also monitor how many 'new and resurrected' node we see in a month, and we'll also follow their behavior in analysis window.
	 - New and resurrected nodes for a month are nodes we are seeing for the first time in observation window. For December cohort, this number is nodes that we didnt see in october and november, and we saw it first time in December. 
	 - Why not just new, why 'new and resurrected'? They could be a resurrected node as well. For example, a node that was active in August, but not active in October, november That node may be joining LN for the first time, or may be after a couple of month of being deactive, it came back to life. We'll get into details of ratio of new and resurrected later on.

## Heat Map

![Cohort Heatmap ]({{ 'assets/Cohortheatmapoctv0.png' | relative_url }})

How to read the heatmap above:


## How many we loose each month

All your files and folders are presented as a tree in the file explorer. You can switch from one to another by clicking a file in the tree.

## Cohort of Currently Active nodes

You can rename the current file by clicking the file name in the navigation bar or by clicking the **Rename** button in the file explorer.

## Nodes behavor based on when they have signed-up

You can delete the current file by clicking the **Remove** button in the file explorer. The file will be moved into the **Trash** folder and automatically deleted after 7 days of inactivity.

## Notes

In general, LN is still an early technology, so a lot of nodes are just Ln enthusiast playing around, and a lot of big nodes are bitcoin business who are here to support the technology  and reap the benefit of being an early adopter. So, in short, dont read too much on data as the behavior will keep changing as the ride along the adoption curve.




<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNjE2NDkzNjAsNzAwMTA3NzkyLDE4NT
c5NjQxMDQsMTM5NjYyMDE1NiwxMjAxNDg1NTI4LDE3NjY5MjI3
MTksMzM4NTQyODM0LC05OTU0ODg4MjksLTMxNTc5NzAsLTMwMj
kyMTI4NywxNTYxNDI2MTgxLDkyMDM2NTIyNiwxNzAxNDczNTI5
LC0xMzMyNDkzNDYzLDk5MTcwMTc0MywtMTk3MjM0MTY3NCwyOT
c4MTYzOV19
-->