---
layout:     post
title:      2020-08-06-How To Understand Strongly/Weekly Connected Component in Graph
subtitle:   Graph
date:       2020-08-06
author:     BY Elon
header-img: img/post-bg-keyboard.jpg
catalog: true
tags:
    - Graph
    - Algorithm
---
Graph usually is denoted by G(V, E), V is set of vertices, E is set of edges.

A directed graph is called **Strongly Connected Graph** if there is a path between all pairs of vertices.

A directed grpah is called **weakly connected** if replacing all of its directed edges with undirected produces a connected undirected graph.

A graph is said to be **minimally connected** if removal of any one edge from it disconnects the graph. Clearly minimally connected graph has no cycles.

Given a directed graph, a weakly connected component(WCC) is a subgraph of original graph where all vertices are connected to each other by some path, ignoring the direction of edges. In case of a undirected graph, a weakly connected component is also a strongly connected component.

1. How to prove a graph is connected?
Given a graph with n vertices, prove that if the degree of each vectex is at least (n-1)/2 then the graph is connected.

2. How to find the largest connected component of a graph? Followup-> Directed Graph
	- Solution1, Use BFS + competition + HashSet; Initialize HashSet with all vertices from Graph. Loop over the HashSet to run BFS, tracing its adjacent vertices and toll its size; Compete and get the largest size.

	- Solution2, Use UnionFind + Competition; 1)Use UnionFind data structure to record all connected component, 2) then peak and choose the largest one

3. Find weakly connected component in a directed graph
	- Similar to 2.) solution2 first part

4. How to prove if there is no cycle in a graph? FollowUp-> In a directed graph?
	- Use BFS to expand node, if there is a node that can be visited twice. It means 