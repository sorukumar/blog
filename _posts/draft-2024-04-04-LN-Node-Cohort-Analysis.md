
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
	 - Why not just new, why 'new and resurrected'? They could be a resurrected node as well. For example, a node that was active in August, but not active in October, november and again start showing up in December is getting counted in December Cohort. What % of these nodes are resurrected? Based on additional data that I have seen, and a rough estimate, 30% of those nodes could be resurrected. We'll do a thourogh anal

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
eyJoaXN0b3J5IjpbLTk5OTM2MjMxLDcwMDEwNzc5MiwxODU3OT
Y0MTA0LDEzOTY2MjAxNTYsMTIwMTQ4NTUyOCwxNzY2OTIyNzE5
LDMzODU0MjgzNCwtOTk1NDg4ODI5LC0zMTU3OTcwLC0zMDI5Mj
EyODcsMTU2MTQyNjE4MSw5MjAzNjUyMjYsMTcwMTQ3MzUyOSwt
MTMzMjQ5MzQ2Myw5OTE3MDE3NDMsLTE5NzIzNDE2NzQsMjk3OD
E2MzldfQ==
-->