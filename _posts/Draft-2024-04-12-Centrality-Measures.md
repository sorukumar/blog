
# Centrality Measures

Centrality measure are metrics to understand, quantify and rank importance of nodes of a graph. Lightning network is a graph.

This is an attemt to define centrality metrics in an intuitive way that would work for even your four legged kid, if you try. I'll also add some thoughts on relevance of the metric in context of Lightning network.
 

## Intuitive definition

1.  **Degree Centrality**
        -   The social butterfly of the network. A node's importance is gauged by how many connections it has. More friends, more central. 
        - So, for lightning network high count of  channels would result into higher degree centrality.
        - If you get connected to a node with high degree centrality with good channel size that is balanced, you are well set to send and receive payments. However, when we are comparing nodes with similar degree centrality, the one that have good channel size, and kept it balance is the one you should choose, even though they may have relatively lower degree centrality.
2.  **Betweenness Centrality**
        -   The broker, the wheel-greaser, the node that lies on the shortest path between others, often controlling the flow of information. If it were a city, it would be Panama—a vital crossroads.
        - This is also a good node to get connected to. However make sure that the canal is wide enough, and secondly, it is quite possible two nodes have same betweenness centrality but they add completely different value to you. Think of Panama and Swej.
3.  **Closeness Centrality**
        -   The node that’s never far from the action, able to whisper in every ear. Measured by how close it stands to every other node in the room, minimizing the whispers needed to spread a secret across the network.
        - what this metrics tells you is that if you have to do mass payments of micro sizes. this is the node to get connected to. The condition of micro size matters because it mimizes the effect of channel size and balanced channel. Mass payments matters because if you expect to send or receive from all almost everyone then it is good metric to look at.
5.  **Eigenvector Centrality**
        -   Not just about having friends, but about having powerful friends. This measure looks at the influence of a node’s connections. In a room full of celebrities, it’s the one who knows the biggest stars.
6.  **Katz Centrality**
        -   Similar to its cousin, the Eigenvector, but adds a sprinkle of influence from all nodes within a few handshakes. It acknowledges even the faintest nod from across the room.
7.  **PageRank**
        -   The algorithm of the Internet age, crafted by Google’s own. Nodes gain status not just by having many connections, but how significant those connections are. It’s the difference between a nod from a king and a wave from a crowd.

# A Network Graph.

```mermaid
flowchart LR
    Sia --- Ria
    Ria --- Xi
    Xi --- Ivy
    Ivy --- Eva
    Sia --- Ivy
    Ria --- Ivy
    Ria --- Eva
   ```
   
## Calculation

#### Degree Centrality

Degree Centrality for a node \(v\) is calculated as:

$\text{Degree Centrality}(v) = \frac{\text{Number of direct connections of } v}{\text{Total possible connections}}$

This measures the immediate connectivity of the node within the network, highlighting its potential for influence or interaction relative to the total network size.




| Node | Degree ( # of nodes connected to) | Calculation                        | Degree Centrality |
|------|--------|------------------------------------|-------------------|
| Sia  | 2      | $\frac{2}{5-1} = \frac{2}{4}$      | 0.5               |
| Ria  | 4      | $\frac{4}{5-1} = \frac{4}{4}$      | 1.0               |
| Xi   | 2      | $\frac{2}{5-1} = \frac{2}{4}$      | 0.5               |
| Ivy  | 4      | $\frac{4}{5-1} = \frac{4}{4}$      | 1.0               |
| Eva  | 2      | $\frac{2}{5-1} = \frac{2}{4}$      | 0.5               |

#### Betweenness Centrality

$\text{Betweenness Centrality}(v) = \frac{\text{Number of shortest paths passing through } v}{\text{Total number of shortest paths}}$


Below table shows shortest path count for each pair.

| Node Pair | Shortest Path Count | Path Details                            | Intermediary Nodes         |
|-----------|---------------------|-----------------------------------------|----------------------------|
| Sia - Ria | 1                   | Direct path                             | None                       |
| Sia - Xi  | 1                   | Path through Ria                        | Ria                        |
| Sia - Ivy | 1                   | Direct path                             | None                       |
| Sia - Eva | 2                   | 1 path through Ivy, 1 path through Ria  | Ivy, Ria                   |
| Ria - Xi  | 1                   | Direct path                             | None                       |
| Ria - Ivy | 1                   | Direct path                             | None                       |
| Ria - Eva | 1                   | Direct path                             | None                       |
| Xi - Ivy  | 1                   | Direct path                             | None                       |
| Xi - Eva  | 1                   | Path through Ivy                        | Ivy                        |
| Ivy - Eva | 1                   | Direct path                             | None                       |
| **Total** | **11**              |                                         |                            |

Once, we have shortest path through each node, and also total shortest path count. below is a table that does calculation on betweenness centrality.


| Node | Shortest Paths Through Node | Betweenness Centrality Calculation | Betweenness Centrality Value |
|------|-----------------------------|-----------------------------------|-----------------------------|
| Sia  | 0                           | $0/11 = 0$                        | 0.0                         |
| Ria  | 2                           | $2/11 \approx 0.182$              | 0.182                       |
| Xi   | 0                           | $0/11 = 0$                        | 0.0                         |
| Ivy  | 2                           | $2/11 \approx 0.182$              | 0.182                       |
| Eva  | 0                           | $0/11 = 0$                        | 0.0                         |
               


#### Closeness Centrality

Closeness Centrality for a node \(v\) is calculated as:
$$
\text{Closeness Centrality}(v) = \frac{\text{Total number of nodes} - 1}{\text{Sum of the shortest path distances from } v \text{ to all other nodes}}
$$
This metric evaluates how quickly a node can reach all other nodes in the network, providing a measure of how 'central' a node is in terms of network navigation.

Calculation for sum of the shortest path

| Node | Paths and Distances                 | Sum of Distances |
|------|-------------------------------------|------------------|
| Sia  | To Ria: 1, To Xi: 2, To Ivy: 1, To Eva: 2 | 6                |
| Ria  | To Sia: 1, To Xi: 1, To Ivy: 1, To Eva: 1 | 4                |
| Xi   | To Sia: 2, To Ria: 1, To Ivy: 1, To Eva: 1 | 5                |
| Ivy  | To Sia: 1, To Ria: 1, To Xi: 1, To Eva: 1  | 4                |
| Eva  | To Sia: 2, To Ria: 1, To Xi: 1, To Ivy: 1  | 5                |

Calculation on Closeness centrality

| Node | Sum of Distances to Other Nodes | Calculation       | Closeness Centrality |
|------|---------------------------------|-------------------|----------------------|
| Sia  | 6                               | $\frac{5-1}{6}$   | 0.67                 |
| Ria  | 5                               | $\frac{5-1}{5}$   | 0.8                  |
| Xi   | 6                               | $\frac{5-1}{6}$   | 0.67                 |
| Ivy  | 5                               | $\frac{5-1}{5}$   | 0.8                  |
| Eva  | 6                               | $\frac{5-1}{6}$   | 0.67                 |



#### Eigenvector Centrality
$\text{Eigenvector Centrality}Ax = \lambda x$

|     | Sia | Ria | Xi  | Ivy | Eva |
|-----|-----|-----|-----|-----|-----|
| Sia |  0  |  1  |  0  |  1  |  0  |
| Ria |  1  |  0  |  1  |  1  |  1  |
| Xi  |  0  |  1  |  0  |  1  |  0  |
| Ivy |  1  |  1  |  1  |  0  |  1  |
| Eva |  0  |  1  |  0  |  1  |  0  |


```mermaid
graph TB
    matrix((Adjacency Matrix))
    rowHeader["| |Sia|Ria|Xi|Ivy|Eva|"]
    row1["|Sia|0|1|0|1|0|"]
    row2["|Ria|1|0|1|1|1|"]
    row3["|Xi|0|1|0|1|0|"]
    row4["|Ivy|1|1|1|0|1|"]
    row5["|Eva|0|1|0|1|0|"]

    matrix --> rowHeader
    rowHeader --> row1
    row1 --> row2
    row2 --> row3
    row3 --> row4
    row4 --> row5
   ```
   

is it overly sensitive

How do you interpret it in terms of opening channels in Lighting network

## A more comprehensive graph

```mermaid
flowchart LR
    Ava --- Mia
    Mia --- Zoe
    Zoe --- Ivy
    Ivy --- Mya
    Mya --- Eva
    Eva --- Ida
    Ida --- Uma
    Uma --- Ava
    Zoe --- Eva
    Mia --- Ida
    Ava --- Uma
    Uma --- Ivy
    Ivy --- Zoe
    Zoe --- Mya
    Mya --- Uma
   ```

## Python code to do centrality measure

## Generic formula for centrality measure for mathematically savvy

$\text{Betweenness Centrality}(v) = \sum_{s \neq v \neq t} \frac{\sigma_{st}(v)}{\sigma_{st}}$

$\text{Degree Centrality}(v) = \frac{\text{Degree of } v}{N-1}$

$\text{Closeness Centrality}(v) = \frac{N-1}{\sum_{u=1}^{N} d(v, u)}$
<!--stackedit_data:
eyJoaXN0b3J5IjpbNjQwOTY3MjAwLC02NTM1MDc5MTAsNjE5MD
I4NDU3LC0xODU0MTkwNDI3LDE0MTQxOTYyNTQsLTE3MDYwMzE0
NjgsLTc5MjM5NjE5OCwxNjE1MTY3NzEyLC0xNDMwNjg3MTk0LD
kzNzE2OTk4MCwxMDk2MjkxOTU2LDY0MDc2NjAyOSwtMTExNjk3
NTAxMCwxODUzNjEwOTc0LDE5NDgyNjA2OTUsLTEzNDYxMTg3MT
UsMTEzMzU5MzUwMywxNTg4NzQ4MjMxLC0yMTM5NTMzMDcyLDM3
NTA3MDk0Nl19
-->