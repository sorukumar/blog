
# Centrality Measures

Centrality measure are metrics to understand networks graphs, like Lighting network.

This is an attemt to define centrality metrics in an intuitive way that would make sense to folks without statistics background, ie for your grand mom.
 

## Intuitive definition

1.  **Degree Centrality**
        -   The social butterfly of the network. A node's importance is gauged by how many connections it has. More friends, more central.
2.  **Closeness Centrality**
        -   The node that’s never far from the action, able to whisper in every ear. Measured by how close it stands to every other node in the room, minimizing the whispers needed to spread a secret across the network.
3.  **Betweenness Centrality**
        -   The broker, the wheel-greaser, the node that lies on the shortest path between others, often controlling the flow of information. If it were a city, it would be Panama—a vital crossroads.
4.  **Eigenvector Centrality**
        -   Not just about having friends, but about having powerful friends. This measure looks at the influence of a node’s connections. In a room full of celebrities, it’s the one who knows the biggest stars.
5.  **Katz Centrality**
        -   Similar to its cousin, the Eigenvector, but adds a sprinkle of influence from all nodes within a few handshakes. It acknowledges even the faintest nod from across the room.
6.  **PageRank**
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

Degree centrality for a node $v$ is given by:

$\text{Degree Centrality}(v) = \frac{\text{Degree of } v}{N-1}$

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




| Node | Shortest Paths Through Node | Betweenness Centrality Calculation | Betweenness Centrality Value |
|------|-----------------------------|-----------------------------------|-----------------------------|
| Sia  | 0                           | $0/12$                        | 0.0                         |
| Ria  | 3                           | $3/12$                     | 0.25                        |
| Xi   | 0                           | $0/12$                        | 0.0                         |
| Ivy  | 3                           | $3/12$                     | 0.25                        |
| Eva  | 0                           | $0/12$                        | 0.0                         |


#### Closeness Centrality

$\text{Closeness Centrality}(v) = \frac{N-1}{\sum_{u=1}^{N} d(v, u)}$
| Node | Sum of Distances to Other Nodes | Calculation       | Closeness Centrality |
|------|---------------------------------|-------------------|----------------------|
| Sia  | 6                               | $\frac{5-1}{6}$   | 0.67                 |
| Ria  | 5                               | $\frac{5-1}{5}$   | 0.8                  |
| Xi   | 6                               | $\frac{5-1}{6}$   | 0.67                 |
| Ivy  | 5                               | $\frac{5-1}{5}$   | 0.8                  |
| Eva  | 6                               | $\frac{5-1}{6}$   | 0.67                 |




$\text{Eigenvector Centrality}Ax = \lambda x$

$\text{Katz Centrality}(v) = \alpha \sum_{j=1}^{n} A_{ij} x_j + \beta$

$\text{PageRank}(p_i) = \frac{1-d}{N} + d \sum_{p_j \in M(p_i)} \frac{\text{PageRank}(p_j)}{L(p_j)}$



## Switch to another file

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

## Rename a file

$\text{Betweenness Centrality}(v) = \sum_{s \neq v \neq t} \frac{\sigma_{st}(v)}{\sigma_{st}}$

$\text{Degree Centrality}(v) = \frac{\text{Degree of } v}{N-1}$
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1OTQ0NzU4NzgsMTk0ODI2MDY5NSwtMT
M0NjExODcxNSwxMTMzNTkzNTAzLDE1ODg3NDgyMzEsLTIxMzk1
MzMwNzIsMzc1MDcwOTQ2LC0xNzk5OTIxMTEyLDE1NTEyMzk1MD
QsLTEyMzExODg2NDgsLTY5ODI2NTI5MCwxMTU0NzUyNTg0LDk4
NTQyNzM3OCwtMjEzMDg1MjY3MCwtOTc4NTMyMDAxLDUxNzE5MT
g1MCw4NjUwMjM2MSw0MDY0NzY3NzcsLTE2NzA0MTk3MTksMjYz
NTE4MDcxXX0=
-->