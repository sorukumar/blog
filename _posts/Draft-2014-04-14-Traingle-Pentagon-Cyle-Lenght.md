
---
layout: post
title: "Traingle or Pentagon -- LN Graph"
categories: Lightning Technical
author:
- sorukumar
---

When you are looking for a peer on LightningNetworkplus, you could either form a traingle or a pentagon. A traingle is formed when 3 nodes open channels to each other, and pentagon is formed when 5 nodes come together to open a channel. here is an example. I have wondered how different or same it is to open a 2 way channel ( dual funded channel), 3 way channel and 5 way channel.

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

```mermaid
graph LR 
	A --- B 
	B --- C 
	C --- A
   ```
```mermaid
graph TB 
	A --- B 
	B --- C 
	C --- A
   ```
5 way channel: Pentagon
```mermaid
graph LR 
	A --- B 
	B --- C 
	C --- D
	C --- A
	C --- A
   ```

The cycle structure of a graph can impact its quality in several ways:

-   Robustness: Longer cycles make the graph more robust, as there are more alternative paths between nodes if some edges fail. Shorter cycles like C3 are more vulnerable.[3](https://math.stackexchange.com/questions/1490053/what-is-the-difference-between-a-loop-cycle-and-strongly-connected-components-i)
-   Routing Efficiency: Longer cycles can allow more efficient routing, as there are more potential paths between nodes. Shorter cycles may limit routing options.[3](https://math.stackexchange.com/questions/1490053/what-is-the-difference-between-a-loop-cycle-and-strongly-connected-components-i)
-   Symmetry: Cycle graphs exhibit high symmetry, as any vertex can be mapped to any other vertex. This symmetry can simplify analysis and algorithms.[2](https://en.wikipedia.org/wiki/Cycle_graph)
1.  Complexity: The problem of finding a single simple cycle that covers each vertex exactly once (a Hamiltonian cycle) is much harder than finding a set of cycles that cover each edge. The length of the cycle affects the complexity of these problems.[1](https://en.wikipedia.org/wiki/Cycle_%28graph_theory%29)
2.  Cycle Detection Algorithms: The algorithms used to detect cycles in a graph, such as depth-first search, can be impacted by the cycle length. Shorter cycles may be easier to detect.[1](https://en.wikipedia.org/wiki/Cycle_%28graph_theory%29)
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzcyMDE2MTc0LC0xMjU0NDMwOTU0LC0xND
M0MzQ4MjI0LC05NzYzODIzMTcsLTE1NzIxOTQ3MjcsLTMxMTQ4
MjgwNiw3MzA5OTgxMTZdfQ==
-->