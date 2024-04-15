
# Centrality Measures for Lightning Network

Centrality measure are metrics to understand, quantify and rank importance of nodes in a graph. Lightning network is a graph.

Here is what I'll try achieving in this post:

 1. Present an intuitive definition and understanding of centrality measures we see around on LN exploreres.
 2. Show and calculate those metrics for a simple 5-node graph
 3. Thoughts on what to think of these centrality metrics when choosing a peer to open a channel.


## Intuitive definition

1.  **Degree Centrality**
        -   The social butterfly of the network. A node's importance is gauged by how many connections it has. More friends, more central. 
 2.  **Betweenness Centrality**
        -   The broker, the wheel-greaser, the node that lies on the shortest path between others, often controlling the flow of information. If it were a city, it would be Panama—a vital crossroads.
        - This is also a good node to get connected to. However make sure that the canal is wide enough, and secondly, it is quite possible two nodes have same betweenness centrality but they add completely different value to you. Think of Panama and Swej.
3.  **Closeness Centrality**
        -   The node that’s never far from the action, able to whisper in every ear. Measured by how close it stands to every other node in the room, minimizing the whispers needed to spread a secret across the network.
        - what this metrics tells you is that if you have to do mass payments of micro sizes. this is the node to get connected to. The condition of micro size matters because it mimizes the effect of channel size and balanced channel. Mass payments matters because if you expect to send or receive from all almost everyone then it is good metric to look at.
4.  **Eigenvector Centrality**
        -   Not just about having friends, but about having powerful friends. This measure looks at the influence of a node’s connections. In a room full of celebrities, it’s the one who knows the biggest stars.


## A Network Graph.

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
   
## Degree Centrality

Degree Centrality for a node \(N\) is calculated as:

$\text{Degree Centrality}(N) = \frac{\text{Number of channels for } N}{\text{Total number of channels in LN graph}}$

For LN, it is only '# of channels' that will have play on degree centrality.  A channel like LQWD-Canada with thousand of channels have 5 times higher degree centrality compared to River, even though River has committed 3 times more bitcoin as liquidity. Refer:[Plebdashboard](https://sorukumar.github.io/plebdashboard/v0:%20for%20feedback/Nodevisualization20240306.html)


**How to think about 'Degree centrality' for node selection?** If you find a node with high D, and not directly connected with you, and if the average channel size is not too low, more or less they are good peer to get started with. We should note that a node may have a good D, but still may not give us good coverage, if all of their channels in concentraed in one part of LN graph.

**Calculation**
| Node | Degree ( # of nodes connected to) | Calculation                        | Degree Centrality |
|------|--------|------------------------------------|-------------------|
| Sia  | 2      | $\frac{2}{5-1} = \frac{2}{4}$      | 0.5               |
| Ria  | 4      | $\frac{4}{5-1} = \frac{4}{4}$      | 1.0               |
| Xi   | 2      | $\frac{2}{5-1} = \frac{2}{4}$      | 0.5               |
| Ivy  | 4      | $\frac{4}{5-1} = \frac{4}{4}$      | 1.0               |
| Eva  | 2      | $\frac{2}{5-1} = \frac{2}{4}$      | 0.5               |

## Betweenness Centrality


$\text{Betweenness Centrality}(N) = \frac{\text{Number of shortest paths passing through } N}{\text{Total number of shortest paths}}$


Below table shows shortest path count for each pair, and it should give you an idea on what is shortest path.

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
               
For LN, it is only '# of channels' that will have play on degree centrality.  A channel like LQWD-Canada with thousand of channels have 5 times higher degree centrality compared to River, even though River has committed 3 times more bitcoin as liquidity. Refer:[Plebdashboard](https://sorukumar.github.io/plebdashboard/v0:%20for%20feedback/Nodevisualization20240306.html)


**How to think about 'Degree centrality' for node selection?** If you find a node with high D, and not directly connected with you, and if the average channel size is not too low, more or less they are good peer to get started with. We should note that a node may have a good D, but still may not give us good coverage, if all of their channels in concentraed in one part of LN graph.


## Closeness Centrality


Closeness Centrality for a node \(v\) is calculated as:

$\text{Closeness Centrality}(v) = \frac{\text{Total number of nodes} - 1}{\text{Sum of the shortest path distances from } v \text{ to all other nodes}}$

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

To calculate the eigenvector centrality of a node \( v \) in a network, we use the following formula:

$\text{Eigenvector Centrality}(v) = \lambda_1 \times \text{Sum of the centralities of the nodes connected to } v$

The best way to solve it is using matrix operation, and iterate over from an assumed value of centrality for each node. 

The whole graph can be represendted as below matrix. it is called adjacency matrics. If you look closely, you will see that, it is nothing but a table, where there is row and column for each node. For n nodes, it is $n by n$ table. if two nodes are connected, we assign 1 to that cell, if they are not connected we assign 0 to the cell.


|     | Sia | Ria | Xi  | Ivy | Eva |
|-----|-----|-----|-----|-----|-----|
| Sia |  0  |  1  |  0  |  1  |  0  |
| Ria |  1  |  0  |  1  |  1  |  1  |
| Xi  |  0  |  1  |  0  |  1  |  0  |
| Ivy |  1  |  1  |  1  |  0  |  1  |
| Eva |  0  |  1  |  0  |  1  |  0  |




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

$\text{Eigenvector Centrality}Ax = \lambda x$
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUxNDIxMTU4LC0xNTI1MzcyOTgsMTMxOD
k0OTkwLDIzNzExMTc0Myw1NzE1MzM1NSwxMjE4Nzk1ODI0LDE5
NDgzODc5NDQsLTIwNjIxNzk0NjYsMTM4MTk4NTQyMyw3NzE5OT
EyOTMsLTY1MzUwNzkxMCw2MTkwMjg0NTcsLTE4NTQxOTA0Mjcs
MTQxNDE5NjI1NCwtMTcwNjAzMTQ2OCwtNzkyMzk2MTk4LDE2MT
UxNjc3MTIsLTE0MzA2ODcxOTQsOTM3MTY5OTgwLDEwOTYyOTE5
NTZdfQ==
-->