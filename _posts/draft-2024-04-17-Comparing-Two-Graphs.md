
#  Health of Lightning network

The best set of metrics to gauge the health of Lighting network graph is actual metrics on [total payment, failure rate and processing time](https://docs.google.com/spreadsheets/d/1N6pCpZLaz-_lRV5K2WmqYq-NFaxfbdB_6aKsiAuEt84/edit?usp=sharing). Considering that info, until all nodes start sharing data is not available, for good reasons. It is important to develop and monitor meaningful metrics that are lead to these metrics, and can work as a proxy.

These metrics come from the graph science literature. And, of course, Lighitng network graph has its own set of constraints and challenges, but, yet it is a good starting point.

In this post, we will lay out the metrics, and eventually, we'll start tracking those in Plebdashboard.

Here is a list of metrics:

### 1. Connectivity Metrics

-   **What is it**:  A well-connected graph ensures that there are multiple paths for transmitting data, which increases the reliability of data transfer.
-   **Metrics**: Look at the number of connected components, the size of the largest connected component, and the average node degree.

### 2. Path Length Metrics

-   **What is it**: The average shortest path length is crucial for data transmission as it affects the speed of communication between any two nodes.
-   **Metrics**: Average shortest path length (mean geodesic distance) and diameter of the graph (the longest of all the shortest path lengths).

### 3. Robustness

-   **What is it**: The ability of the graph to maintain connectedness and functionality when nodes or edges fail.
-   **Metric**: Measure the graph's resilience by simulating node or edge failures and observing how the graph's connectivity and average path length are affected.

### 4. **Throughput**

-   **What is it**: The graph’s capacity to handle large amounts of data simultaneously without significant delays.
-   **Metric**: This can be indirectly measured by analyzing the graph’s degree distribution and bandwidth (which might be theoretical in some cases unless specified by the network’s physical or software design).

### 5. **Network Efficiency**

-   **What is it**: Overall efficiency of the network in terms of both local and global efficiency.
-   **Metric**: Global efficiency (inverse of the average shortest path length) and local efficiency (measures efficiency of information transfer in localized clusters).

### 6. **Clustering Coefficient**

-   **What is it**: Indicates the degree to which nodes in the graph tend to cluster together. High clustering can suggest robustness, as parallel paths can exist for data transmission.
-   **Metric**: Global and average local clustering coefficients.

### 7. **Centrality Measures**

-   **What is it**: Important to identify critical nodes for maintaining fast and reliable communication.
-   **Metric**: Degree centrality (for node importance), betweenness centrality (nodes critical for bridging paths), and closeness centrality (nodes efficiently distributing data).

### 8. **Scalability**

-   **What is it**: How well can the network grow? This is particularly important if the network needs to accommodate more nodes or heavier data flow without significant performance degradation.
-   **Metric**: This is more of a qualitative assessment, looking at how adding nodes or edges affects the metrics mentioned above.

### 9. **Load Balancing**

-   **What is it**: The ability of the network to distribute traffic evenly among nodes to prevent any single node from becoming a bottleneck.
-   **Metric**: Variance in node degree and edge loads can be simulated under various traffic conditions to observe potential bottlenecks.



<!--stackedit_data:
eyJoaXN0b3J5IjpbMTEyNjY3NDMzNCw2ODc4ODMyMDksLTgxNj
g4MjY5NiwtMTg1MjQwMDU5OCwtMjAwNDE2NDE5OCwxNDcyNDc1
Mzk3XX0=
-->