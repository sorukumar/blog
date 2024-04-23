
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

The goal of this post is to share data, and provide some interpretation. In the next iteration of cohort analysis, I'll pass more holistic analysis and story.


# The data & Methodology

We have LN graph output from an LND node since May-2023. We are analysing graph data pulled on a day of the first week for following months. Here is how the data looks.


![# of LN Node]({{ 'assets/2by2BitcoinbizMar20.png' | relative_url }})


#of Nodes is unique pub key in the from the graph output. But depending on who  we want to count as nodes, lets define active node as well.
Active nodes: Nodes with at least one active public channel that has sent at least one update.

Please note that:

 - I dont have data for june, July and September. So, for our puspose, we'll analyze 9 months of data to to understand cohort behavior
 - We'll focus our analysis on only active nodes.
 - Methodology: 
	 - We'll look at all active nodes in a month, and continue monitoring how many of 		them are active in subsequent months
	 - In the heatmap below, we are following nodes from October 2023. Any node that LN graph didnt see in october and say in November is 'New or resurrected' for November. 

## Heat Map



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
eyJoaXN0b3J5IjpbMTM5NjYyMDE1NiwxMjAxNDg1NTI4LDE3Nj
Y5MjI3MTksMzM4NTQyODM0LC05OTU0ODg4MjksLTMxNTc5NzAs
LTMwMjkyMTI4NywxNTYxNDI2MTgxLDkyMDM2NTIyNiwxNzAxND
czNTI5LC0xMzMyNDkzNDYzLDk5MTcwMTc0MywtMTk3MjM0MTY3
NCwyOTc4MTYzOV19
-->