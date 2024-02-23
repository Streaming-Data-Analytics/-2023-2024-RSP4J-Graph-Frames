# 2023-2024 RSP4J Graph Frames

Optional #project of the [Streaming Data Analytics](http://emanueledellavalle.org/teaching/streaming-data-analytics-2022-23/) course provided by [Politecnico di Milano](https://www11.ceda.polimi.it/schedaincarico/schedaincarico/controller/scheda_pubblica/SchedaPublic.do?&evn_default=evento&c_classe=811164&polij_device_category=DESKTOP&__pj0=0&__pj1=1b82965d3c68857e2087d3f3b98a9e40).
### Prerequisites

- Java Programming
	- Java 8+
	- MVN
- Functional Programming (basics)
## Description 

Traditional Data Stream Management Systems (DSMS) break down data streams into sections using windows based on time intervals or specific amounts of data. These windows are set in place and don't change, even if the data stream itself changes over time, like getting faster or slower, or the kind of data being streamed changes.

However, since data streams can change in how fast data comes in or what the data is about, sticking to one way of breaking down the streams doesn't always work well. This is why we need a new, more flexible way to divide up data streams.

Grossniklaus et al.  introduced a new method called _frames_. Unlike the old way, frames divide streams based on what's in the data itself. We've developed a theory and a way to use frames, and we'll show how frames can be really useful for different kinds of applications.


## Project Goal 

This project aims at designing and implementing a new notion of frames, which directly based on [[#Graph-specific aggregations]], within RSP4J library.


## Requirements

Graph-specific aggregations are operations that summarise information from a graph's structure, including its nodes, edges, and their attributes. These aggregations are crucial for understanding complex networks and for tasks like graph analytics, network analysis, and feature engineering in machine learning. Below there is a list of interesting graph aggreagtion.

The project consist in studying what aggregations are most promising for the definition of graph-based frames.  Relevant for the project is understanding the concept of Frames below, with a particular focus on Aggregate Frames, which are window policy that take as input a function chuck the stream into finite portions wrt such function. *E.g., window every time the sum goes above a certain constant.* 

![[frames.png]]

### RSP4J Library

RSP4J is a library to build RDF Stream Processing (RSP) Engines according with the reference model RSP-QL. RDF is a graph data model for the Web. RDF streams are infinite sequences of RDF timestamped RDF data. The library  is inspired by the OWL API, and attempt to uniform the access to existing RDF-based DSMS. 

In this [repository](https://github.com/streamreasoning/rsp4j), you will find several projects, including

- API, which contains the interfaces and abstractions required to develop your RSP engine.
- yasper, which is an reference implementation that aims at showing the API usage by providing org.streamreasoning.rsp4j.yasper.examples.
- examples to understand the genral functioning of RSP4K

### Graph-specific aggregations 

Here's a list of some common graph-specific aggregations:

1. **Degree Centrality Aggregation**: This calculates the number of connections (edges) each node has. It can be further divided into in-degree (number of incoming edges) and out-degree (number of outgoing edges) for directed graphs.
2. **Closeness Centrality Aggregation**: This measures how close a node is to all other nodes in the graph, based on the shortest paths connecting them.
3. **Betweenness Centrality Aggregation**: This identifies nodes that serve as bridges within the graph. It measures the number of times a node lies on the shortest path between other node pairs.
5. **Clustering Coefficient Aggregation**: Measures how close a node and its neighbors are to being a complete graph (a set of nodes where every node is connected to every other node).
7. **Eigenvector Centrality**: Similar to PageRank but considers the centrality of neighboring nodes. A node is considered important if it is connected to other important nodes.
8. **Density**: Measures the proportion of potential connections in a graph that are actual connections, giving an idea of how dense the graph is.
9. **Path Length Aggregation**: Involves computing the shortest paths between nodes and can include measures like the average path length, which gives an idea of how interconnected a graph is.
10.  Path Expressions require detecting path that follow a certain length or maximizing/minimising path with a given structure.
11. **Connected Components**: Identifies subsets of nodes within a graph that are connected to each other, but not connected to nodes in other subsets.
12. **Graph Diameter**: The largest number of vertices that must be traversed in order to travel from one node to another when paths which are the shortest are chosen.
13. **Neighborhood Aggregation**: Summarizes attributes or metrics of neighboring nodes, often used in graph neural networks for feature aggregation.

## Material

### JGraphT

JGraphT is an open-source Java class library which not only provides us with various types of graphs but also many useful algorithms for solving most frequently encountered graph problems.

It is not mandatory to use it in the project, but could be a good starting point.


### RSP4J

In this [repository](https://github.com/streamreasoning/rsp4j), you will find several information about RSP4J, including

- API, which contains the interfaces and abstractions required to develop your RSP engine.
- Yasper, which is an reference implementation that aims at showing the API usage by providing org.streamreasoning.rsp4j.yasper.examples.
- examples to understand the general functioning of RSP4J

#### Window Operators in RSP4J

RSP4J combines the logic of CQL and SECRET. It identified operators according to three families (see figure below)

![[cql.png]]

The internals of window operator follow the logic of SECRET. They are operationalised according to four functions: tick, scope, content, and report. The operations needs to be redefined for incorporating the Frame semantics. Example of existing implementation for time-based sliding windows are linked below.

- [Example from C-SPARQL](https://github.com/streamreasoning/rsp4j/wiki/C-SPARQL-SLIDING-WINDOW-OPERATOR)
- [Example from CQELS](https://github.com/streamreasoning/rsp4j/wiki/CQELS-SLIDING-WINDOW-OPERATOR)

### Datasets

The project should work with two datasets, 

- [DEBS Challenge 2017](https://ckan.project-hobbit.eu/dataset/debs-grand-challenge-2017)
- New York City Taxi,  by representing the data in RDF
- and a synthetic dataset to be created for the test cases.

## References

- [Frames](https://kops.uni-konstanz.de/server/api/core/bitstreams/55c23a7a-242f-4530-bee9-b2597fb5b76a/content)
- [RSP4J](https://openreview.net/pdf?id=IbXJmD1i2WA)
- [https://jgrapht.org/](https://jgrapht.org/)
