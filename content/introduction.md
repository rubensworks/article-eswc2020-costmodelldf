## Introduction
{:#introduction}


Knowledge Graphs (KGs) become vital assets to provide scalable knowledge models that allow end users to represent, search and explore facts about entities and discover relationships and connections among them which could be challenging to observe in real life. Most Web Knowledge Graphs are created on, following Linked Data (LD) standards, based on RDF data model for publishing and SPARQL as a querying language. 

The rapid growth of open and decentralized Knowledge Graphs over the Web have created an immense demand for public Knowledge Graph query service. However, enabling live queryable Knowledge Graphs on the Web is hardly possible due to the well-known low availability and expensive hosting of SPARQL endpoints despite their impressive query capabilities. On the other hand, offering offline data dumps does not lead us to the desired reliable Web querying to the public Knowledge Graphs regardless of the their low-cost server hosting.

Alternatively Linked Data Fragments (LDF), introduced the foundation of a framework that urges the research the direction of exploring the range of potential Web querying interfaces that come between the woe extremist solutions. LDF aims to investigate the pros and cons of solutions that distribute and balance the load of the query execution between the clients and the server. 

In the following, we provide a brief summary for the approaches that have followed the proposed LDF framework:


⋅⋅* Triple Pattern Fragment (TPF): TPF is a Web Knowledge Graph interface that allows live SPARQL querying to Open Knowledge Graphs with high availability and scalability. TPF reduces the server load and increases the caching by restricting the server capabilities to only answer single pattern fragments and shifting the query processing to the client-side but with the expenses of a substantial increase in the network traffic and slower query execution performance.
⋅⋅* Bindings-Restricted Triple Pattern Fragments (brTPF): brTPF reduces the incurred network load through attaching triple patterns with bindings from previously evaluated triple patterns. brTPF ensures fewer request to the server plus faster query processing. However brTPF, struggles with high number of concurrent clients, queries with large intermediate results and massive Knowledge Graphs.
⋅⋅* SaGe: is designed to provide a starvation-free public SPARQL query service based on a Web Preemption approach. SaGe prevents complex queries from sewing up the server resources by suspending the running query after fixed time quantum with the possibility of resuming the query execution upon the client request. In addition, SaGe defines list of SPARQL operators that are executed on the client-side. Experiments showed that SaGe has improved the average query completion time with the advantage of reducing the network load. On the other hand, SaGe is heavily exhausting the server resources and incurs query performance degradation with increasing number of clients and large-size Knowledge Graphs. 
⋅⋅* smart-KG: is a new paradigm that introduces incorporating approaches that follow Linked Data Fragment framework in order to resolve server-side load-imbalance in large scale Web Knowledge Graph querying. smart-KG proposes a hybrid-shipping approach through shipping indexed, compressed and queryable graph partitions which are created using HDT and based on Family-Based partitioning derived from \emph{characteristic sets} with intermediate results of single triple patterns using TPF.
Experiments showed that smart-KG outperforms the currently existing public Knowledge Graph query engines in the case of massive numbers of concurrent clients and billion-size KGs. However, we believe that there is a room for a more balanced client-server distribution in a way that could achieve higher query performance and less network traffic.



The main objective of this research is to provide a more intelligent interface that benefits from the variety of capabilities of the currently existing query interfaces through introducing double-side (client/server) cost models. Thus the proposed interface will insure that that the server and the clients resources are well-utilized in order to achieve the highest possible query performance with the current available sever resources. 

A preliminary client approach sought to introduce a heuristic method that exploits the characteristics of the different available interfaces. Another proposal suggests a server that provide multiple query services that will serve the clients according to the current status of the server workload. However, there is no concrete cost-model proposal that regulates the client and server negotiations in order to achieve the highest feasible query execution performance with the current server availability.

In this paper, we plan to implement our double-side (client/server) cost models on top of Comunica which is a flexible query engine platform which supports multiple heterogeneous interfaces. Comunica introduced Actor-Mediator-Bus Pattern that will allow us to integrate multiple Knowledge Graph  interfaces.

Definitely cite these papers:
* LDF+TPF, SmartKG(?), Sage
* [Towards More Intelligent SPARQL Querying Interfaces](https://cpb-ap-se2.wpmucdn.com/blogs.auckland.ac.nz/dist/b/412/files/2019/10/paper_421.pdf)
    Problem: No concrete proposals
* [Intelligent Clients for Replicated Triple Pattern Fragments](https://link.springer.com/chapter/10.1007/978-3-319-93417-4_26)
    Problem: Only for replicated TPF interfaces, not combining different LDFs.
* Comunica
{:.todo}

problem: different interfaces have pros/cons -> there's no way of combining them (based on params, load, ...)
solution: 2 cost-models: server and client
{:.todo}
