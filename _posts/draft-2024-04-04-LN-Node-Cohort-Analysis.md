
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


#of Nodes is count of unique pub key in the from the graph output. But depending on who  we want to count as nodes, lets define active node as well.
Active nodes: Nodes with at least one active public channel that has sent at least one update.

Please note that:

 - I dont have data for june, July and September. So, for our puspose, we'll analyze 9 months of data to to understand cohort behavior
 - We'll focus our analysis on only active nodes.

**Methodology:** 
	 - We'll look at all active nodes in a month, and continue monitoring how many of 		them are active in subsequent months
	 - In the heatmap below, we are following nodes from October 2023. Any node that LN graph didnt see in october and say in November is 'New or resurrected' for November. 
	 - Why not just new, why 'new and resurrected'? A node seen first time in November, and not seen in October what we see in that row. That node may be joining LN for the first time, or may be after a couple of month of being deactive, it came back to life. We'll get into details of ratio of new and resurrected later on.

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
eyJoaXN0b3J5IjpbMTY1NjQ4NTI1MCw3MDAxMDc3OTIsMTg1Nz
k2NDEwNCwxMzk2NjIwMTU2LDEyMDE0ODU1MjgsMTc2NjkyMjcx
OSwzMzg1NDI4MzQsLTk5NTQ4ODgyOSwtMzE1Nzk3MCwtMzAyOT
IxMjg3LDE1NjE0MjYxODEsOTIwMzY1MjI2LDE3MDE0NzM1Mjks
LTEzMzI0OTM0NjMsOTkxNzAxNzQzLC0xOTcyMzQxNjc0LDI5Nz
gxNjM5XX0=
-->