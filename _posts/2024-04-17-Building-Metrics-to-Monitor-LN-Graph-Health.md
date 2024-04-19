---
layout: post
title: "Building Metrics to Measure Health of Lightning Network Graph v0.0"
categories: Lightning Technical
author:
- sorukumar
---

The best set of metrics to gauge the health of Lighting network graph is actual metrics on [total payment, failure rate and processing time](https://docs.google.com/spreadsheets/d/1N6pCpZLaz-_lRV5K2WmqYq-NFaxfbdB_6aKsiAuEt84/edit?usp=sharing). Considering that info, for good reasons, is not available until all nodes start sharing data. It is important to develop and monitor meaningful metrics that can work as a proxy.  If the newly defined metrics is lead to 

These metrics come from the graph literature. [Link1](https://reference.wolfram.com/language/guide/GraphMeasures.html) . LN graph has its own set of constraints and challenges, so the [metrics needs to defined](https://link.springer.com/chapter/10.1007/978-3-642-23780-5_13) for it.

In this post, I will lay out the metrics category. I'll come up and share the precise metrics definition after diving deep into the data along with the below metrics dimension.

Here is a list of metrics:

### 1. Connectivity Metrics

-   **What is it**:  It checks that there are multiple path from node A to node B.
-   **Metrics**: Look at the number of 'well' connected components, the size of the largest connected component, and the average node degree.

### 2. Path Length Metrics

-   **What is it**: The average shortest path length is crucial for HTLC transmission. Remember liquidity is an unknown for us.  The more number of channels the more number of unknows in terms of liquidity balance.
-   **Metrics**: distribution of Average shortest path length (mean geodesic distance) and diameter of the graph (the longest of all the shortest path lengths) for active nodes.

### 3. Robustness

-   **What is it**: The ability of the graph to maintain connectedness and functionality when nodes or edges fail.
-   **Metric**: Measure the graph's resilience by simulating node or edge failures and observing how the graph's connectivity and average path length are affected.

### 4. Throughput

-   **What is it**: The graph’s capacity to handle large amounts of data simultaneously without significant delays.
-   **Metric**: This can be indirectly measured by analyzing the graph’s degree distribution and bandwidth.

### 5. Network Efficiency

-   **What is it**: Overall efficiency of the network in terms of both local and global efficiency. The ability of the network to distribute traffic evenly among nodes to prevent any single node from becoming a bottleneck
-   **Metric**: Global efficiency (inverse of the average shortest path length) and local efficiency (measures efficiency of information transfer in localized clusters). Variance in node degree and edge loads can be simulated under various traffic conditions to observe potential bottlenecks

### 6. Clustering Coefficient

-   **What is it**: Indicates the degree to which nodes in the graph tend to cluster together. High clustering can suggest robustness, as parallel paths can exist for data transmission.
-   **Metric**: Global and average local clustering coefficients.

### 7. Centrality Measures

-   **What is it**: Important to identify critical nodes for maintaining fast and reliable communication.
-   **Metric**: Degree centrality (for node importance), betweenness centrality (nodes critical for bridging paths), closeness centrality (nodes efficiently distributing data), and eigenvector centrality (node influence through high-quality connections).
<!--stackedit_data:
eyJoaXN0b3J5IjpbOTkxMzgxNjIxLDQ2NTA0NjU5LDEwNjk1OT
AzOTVdfQ==
-->