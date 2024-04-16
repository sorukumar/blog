


$\text{Katz Centrality}(v) = \alpha \sum_{j=1}^{n} A_{ij} x_j + \beta$

$\text{PageRank}(p_i) = \frac{1-d}{N} + d \sum_{p_j \in M(p_i)} \frac{\text{PageRank}(p_j)}{L(p_j)}$


This is an attemt to define centrality metrics in an intuitive way that would work for even your four legged kid, if you try. I'll also add some thoughts on relevance of the metric in context of Lightning network.

6.  **Katz Centrality**
        -   Similar to its cousin, the Eigenvector, but adds a sprinkle of influence from all nodes within a few handshakes. It acknowledges even the faintest nod from across the room.
7.  **PageRank**
        -   The algorithm of the Internet age, crafted by Google’s own. Nodes gain status not just by having many connections, but how significant those connections are. It’s the difference between a nod from a king and a wave from a crowd.


get connected to a node with high degree centrality with good channel size that is balanced, you are well set to send and receive payments. However, when we are comparing nodes with similar degree centrality, the one that have good channel size, and kept it balance is the one you should choose, even though they may have relatively lower degree centrality


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
eyJoaXN0b3J5IjpbLTE4ODIyNDI0MjVdfQ==
-->