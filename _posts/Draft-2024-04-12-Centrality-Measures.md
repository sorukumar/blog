
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


**How to think about 'Degree centrality' for node selection?** If you find a node with high D, and not directly connected with you, and if the average channel size is not too low, more or less they are good peer to get started with. We should note that a node may have a good D, but still may not give us good coverage, if all of their channels in concentraed in one part of LN graph. Make a note that capacity/liquidity has no play on this metric.

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
               
It is not just the count of channel matters for high B, but the location of node in the graph. A node with a low channel count (low D) may have high B, if it acts as a bridge.  

For an example, have a look at below graph. Kim has high B, even though we have nodes with high D.
```mermaid
flowchart LR
    Alice --- Bob
    Bob --- Carol
    Carol --- Alice
    Dave --- Eve
    Eve --- Frank
    Frank --- Dave
    Alice --- Kim
    Kim --- Dave
   ```

**How to think about 'Betweenness centrality' for node selection?** In general, it is great connecting to a bridge, as it gives you a very good coverage. However, make a note again that capacity/liquidity has no play on this metric.

## Closeness Centrality

Closeness Centrality for a node \(N\) is calculated as:

$\text{Closeness Centrality}(N) = \frac{\text{Total number of nodes} - 1}{\text{Sum of the shortest path distances from } N \text{ to all other nodes}}$

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

```mermaid
flowchart TB
    HighBetweennessNode --- NodeA
    HighBetweennessNode --- NodeB
    NodeA --- HighDegreeNode
    NodeB --- NodeC
    HighDegreeNode --- NodeD
    HighDegreeNode --- NodeE
    HighDegreeNode --- NodeF
    NodeC --- NodeG
    NodeC --- NodeH
    NodeG --- NodeH
    HighClosenessNode --- HighDegreeNode
    HighClosenessNode --- NodeC
    HighClosenessNode --- HighBetweennessNode
   ```

**Lightning and Closeness centrality:** Looking at the graph, you may guess that 'HighbetweennessNode' does not have super low closeness centrality. There is a overlappall with other meausre of centrality, so in the contxt of LN, we dont get the incremental value from additional calculation. However, if someone is doing micro mass payment, this would be the node to get connected to. Micro payment makes sure that we dont have to worry about liquidity a lot, mass payment because, through this node, you can connect to eveyone in the graph with least hops.


#### Eigenvector Centrality

To calculate the eigenvector centrality of a node \( N \) in a network, we use the following formula:

$\text{Eigenvector Centrality}(v) = \lambda_1 \times \text{Sum of the centralities of the nodes connected to } N$

The solve of the above problem has to be iterative, the centrality of node $N$ depdends on its neighbors, and each neighbors centrality depends on all its neighbors that includes $N$. We'll embark on presenting above equation as matrix form as it would bvery effective in solving for this iterative problem

Mathematically, we can say the centrality $x_{N}$ of node $N$:
$x_N = \frac{1}{\lambda} \sum_{M \in \text{Neighbors}(N)} x_M$

Incorporating the adjacency matrix $A$, where $n$ is the total number of nodes, and $a_{NM}$ is an element of the adjacency matrix indicating the presence or absence of a link between $N$ and $M$.
Expressing the centrality using matrix notation for all nodes
$x_N = \frac{1}{\lambda} \sum_{M=1}^{n} a_{NM} x_M$

Multiply through by $λ$ and rearrange the equation:
$x = \frac{1}{\lambda} Ax$

Final expression in matrix equation form:
$\text{Eigenvector Centrality}Ax = \lambda x$


The 5-node graph we are working on, can be represented as below table. When represented as matrix, it is called adjacency matrix $A$ . You may notice that  there is a row and a column for each node. For n nodes, it is $n * n$ table. if two nodes are connected, we assign 1 to that cell, if they are not connected we assign 0 to the cell. Simple.

|     | Sia | Ria | Xi  | Ivy | Eva |
|-----|-----|-----|-----|-----|-----|
| Sia |  0  |  1  |  0  |  1  |  0  |
| Ria |  1  |  0  |  1  |  1  |  1  |
| Xi  |  0  |  1  |  0  |  1  |  0  |
| Ivy |  1  |  1  |  1  |  0  |  1  |
| Eva |  0  |  1  |  0  |  1  |  0  |

$\text{Adjacency Matrix } A = \begin{bmatrix}0 & 1 & 0 & 1 & 0 \\1 & 0 & 1 & 1 & 1 \\0 & 1 & 0 & 1 & 0 \\1 & 1 & 1 & 0 &1\\0 & 1 & 0 & 1 & 0 \\\end{bmatrix}$


Now, we know what  $A$ is we can  solve for  centrality vector $x$ in the equation $Ax = \lambda x$ with an initial guess of 
$x^{(0)} = \begin{bmatrix} 1 \\ 1 \\ 1 \\ 1 \\ 1 \end{bmatrix}$
  

| Iteration | Vector $x$                                    | Norm of $x$      | Normalized $x$                                                                                           | Approx. $\lambda$   | $\lambda$ Formula                      |
|-----------|------------------------------------------------|------------------|---------------------------------------------------------------------------------------------------------|---------------------|---------------------------------------|
| Initial   | $[1, 1, 1, 1, 1]^T$                           | $\sqrt{5}$       | $[1, 1, 1, 1, 1]^T$                                                                                     | -                   | -                                     |
| 1         | $[2, 4, 2, 4, 2]^T$                           | $2\sqrt{11}$     | $\left[\frac{1}{\sqrt{11}}, \frac{2}{\sqrt{11}}, \frac{1}{\sqrt{11}}, \frac{2}{\sqrt{11}}, \frac{1}{\sqrt{11}}\right]^T$ | $2\sqrt{11}$ (6.633)| $\lambda \approx \frac{\|x^{(1)}\|}{\|x^{(0)}\|} = \frac{2\sqrt{11}}{\sqrt{5}}$ |

Now, we know how to calculate eigenvector centrality, have a look at a graph below that show 

```mermaid
flowchart TB
    HighBetweennessNode --- NodeA
    HighBetweennessNode --- NodeB
    NodeA --- HighDegreeNode
    NodeB --- NodeC
    HighDegreeNode --- NodeD
    HighDegreeNode --- NodeE
    HighDegreeNode --- HighEigenvectorNode
    HighEigenvectorNode --- HighClosenessNode
    HighClosenessNode --- NodeD
    HighClosenessNode --- NodeE
    NodeC --- NodeG
    NodeC --- NodeH
    NodeG --- NodeH
    HighEigenvectorNode --- NodeF
    NodeF --- NodeG
   ```

is it overly sensitive

How do you interpret it in terms of opening channels in Lighting network



<!--stackedit_data:
eyJoaXN0b3J5IjpbODIyMDg0MzcsLTc3MTQ3MzQ3NCwtMTk1NT
kwNzQxOSwxNTExNTY2MjgxLDgyMDQ2MTI2OSwxNDMyMTg0OTE1
LC0xNTgyMTk2MDM0LC0xNTY0MzMyNTMxLC0yNTY4MDM0ODIsMT
kyMDI3Mjg1NCw1ODA0MjA0NTIsMjMwNDkxMDA5LDExMDgzNjAz
MDMsLTk3Njg4MjMyLC0xNTI1MzcyOTgsMTMxODk0OTkwLDIzNz
ExMTc0Myw1NzE1MzM1NSwxMjE4Nzk1ODI0LDE5NDgzODc5NDRd
fQ==
-->