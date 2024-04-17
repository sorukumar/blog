
---
layout: post
title: "Traingle or Pentagon -- LN Graph"
categories: Lightning Technical
author:
- sorukumar
---

When you are looking for a peer on LightningNetworkplus, you could either form a traingle or a pentagon. 

2 way channel
```mermaid
graph LR 
	A --- B 
   ```
3 way channel: Traingle
```mermaid
flowchart LR 
	A --- B 
	B --- C 
	C --- A
   ```
5 way channel: Pentagon
```mermaid
flowchart LR 
	A --- B 
	B --- C 
	C --- D
	D --- E
	E --- A
   ```

I have wondered how different or same it is to open a 2 way channel, 3 way channel and 5 way channel.

First, lets establish, how we will look to compare them.

We can compare them along two dimensions. 1st dimention would be how good it is for node operators, 2nd dimentions would be how good it is for whole network.

For node operators, the defnition of 'good' is  succesful routing through the node, and for the whole network the defintion of good is lower payment failure rate for the network.

Conisdering, we don't have data for either. We'll look for its proxies.



The cycle structure of a graph can impact its quality in several ways:

-   Robustness: Longer cycles make the graph more robust, as there are more alternative paths between nodes if some edges fail. Shorter cycles like C3 are more vulnerable.[3](https://math.stackexchange.com/questions/1490053/what-is-the-difference-between-a-loop-cycle-and-strongly-connected-components-i)
-   Routing Efficiency: Longer cycles can allow more efficient routing, as there are more potential paths between nodes. Shorter cycles may limit routing options.[3](https://math.stackexchange.com/questions/1490053/what-is-the-difference-between-a-loop-cycle-and-strongly-connected-components-i)
-   Symmetry: Cycle graphs exhibit high symmetry, as any vertex can be mapped to any other vertex. This symmetry can simplify analysis and algorithms.[2](https://en.wikipedia.org/wiki/Cycle_graph)
1.  Complexity: The problem of finding a single simple cycle that covers each vertex exactly once (a Hamiltonian cycle) is much harder than finding a set of cycles that cover each edge. The length of the cycle affects the complexity of these problems.[1](https://en.wikipedia.org/wiki/Cycle_%28graph_theory%29)
2.  Cycle Detection Algorithms: The algorithms used to detect cycles in a graph, such as depth-first search, can be impacted by the cycle length. Shorter cycles may be easier to detect.[1](https://en.wikipedia.org/wiki/Cycle_%28graph_theory%29)





A traingle is formed when 3 nodes open channels to each other, and pentagon is formed when 5 nodes come together to open a channel. here is an example. 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTY2NzY4MTI5OSwxODIyNDE3MjU3LC0xMj
U0NDMwOTU0LC0xNDM0MzQ4MjI0LC05NzYzODIzMTcsLTE1NzIx
OTQ3MjcsLTMxMTQ4MjgwNiw3MzA5OTgxMTZdfQ==
-->