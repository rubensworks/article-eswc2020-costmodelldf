## Introduction
{:#introduction}

{:.comment data-author="RT"}
This intro may be a bit too high-level, everyone at the conference will already know this stuff :-)
I guess we can just introduce KGs in a sentence or so, and them immediately try to focus on the problem of publishing KGs on the Web, and motivating why a cost model is needed.

Knowledge Graphs (KGs) become vital assets to provide scalable knowledge models that allow end users to represent, search and explore facts about entities and discover relationships and connections among them which could be challenging to observe in real life. Most Web Knowledge Graphs <span class="rephrase">are created on</span>, following [Linked Data (LD) standards](cite:cites linkeddata), based on RDF data model for publishing and SPARQL as a querying language.

The rapid growth of open and decentralized Knowledge Graphs over the Web have created an immense demand for public Knowledge Graph query services. However, enabling live queryable Knowledge Graphs on the Web is hardly possible due to the <span class="reference needed">well-known low availability and expensive hosting of SPARQL endpoints despite their impressive query capabilities</span>. On the other hand, offering offline data dumps does not lead us to the desired reliable Web querying to the public Knowledge Graphs regardless of the their low-cost server hosting.

Alternatively, [Linked Data Fragments (LDF)](cite:cites verborgh_jws_2016) introduced the foundation of a framework that urges the research the direction of exploring the range of potential Web querying interfaces that come between the woe extremist solutions. LDF aims to investigate the pros and cons of solutions that distribute and balance the load of the query execution between the clients and the server. 

{:.comment data-author="RT"}
While the summary below is valuable, I'm afraid we don't have the space for it in this poster paper.
We should definitely mention each one of them, but restrict their explanation to at most 1 (short) sentence each.
If we can combine them in fewer sentences, that's even better :-)

In the following, we provide a brief summary for the approaches that have followed the proposed LDF framework:

* [Triple Pattern Fragment (TPF)](cite:cites verborgh_jws_2016): TPF is a Web Knowledge Graph interface that allows live SPARQL querying to Open Knowledge Graphs with high availability and scalability. TPF reduces the server load and increases the caching by restricting the server capabilities to only answer single pattern fragments and shifting the query processing to the client-side but with the expenses of a substantial increase in the network traffic and slower query execution performance.

* [Bindings-Restricted Triple Pattern Fragments (brTPF)](cite:cites brTPF): brTPF reduces the incurred network load through attaching triple patterns with bindings from previously evaluated triple patterns. brTPF ensures fewer request to the server plus faster query processing. However brTPF, struggles with high number of concurrent clients, queries with large intermediate results and massive Knowledge Graphs.

* [SaGe](cite:cites minier2019sage): is designed to provide a starvation-free public SPARQL query service based on a Web Preemption approach. SaGe prevents complex queries from sewing up the server resources by suspending the running query after fixed time quantum with the possibility of resuming the query execution upon the client request. In addition, SaGe defines list of SPARQL operators that are executed on the client-side. Experiments showed that SaGe has improved the average query completion time with the advantage of reducing the network load. On the other hand, SaGe is heavily exhausting the server resources and incurs query performance degradation with increasing number of clients and large-size Knowledge Graphs. 

* [smart-KG](cite:cites smartKG): is a new paradigm that introduces incorporating approaches that follow Linked Data Fragment framework in order to resolve server-side load-imbalance in large scale Web Knowledge Graph querying. smart-KG proposes a hybrid-shipping approach through shipping indexed, compressed and queryable graph partitions which are created using [HDT](cite:cites fern-etal-2013-HDT-JWS) and based on Family-Based partitioning derived from characteristic sets with intermediate results of single triple patterns using TPF.
Experiments showed that smart-KG outperforms the currently existing public Knowledge Graph query engines in the case of massive numbers of concurrent clients and billion-size KGs. However, we believe that there is a room for a more balanced client-server distribution in a way that could achieve higher query performance and less network traffic.

{:.comment data-author="RT"}
The paragraph below needs more motivation and explanation.
It should clarify why cost models are needed exactly (what is the problem), and how they solve the problem.

The main objective of this research is to provide a more intelligent interface that benefits from the variety of capabilities of the currently existing query interfaces through introducing double-side (client/server) cost models. Thus the proposed interface will insure that that the server and the clients resources are well-utilized in order to achieve the highest possible query performance with the current available sever resources. 

{:.comment data-author="RT"}
These client and server negotiations need some more details.
Why are they needed exactly? (because multiple server interfaces may be available under a certain server load, and the client needs a way to intelligently choose one of them)

A [preliminary client approach](cite:cites hetero) sought to introduce a heuristic method that exploits the characteristics of the different available interfaces. [Another proposal](cite:cites khanISWC2019) suggests a server that provides multiple query services that will serve the clients according to the current status of the server workload. However, there is no concrete cost-model proposal that regulates the client and server negotiations in order to achieve the highest feasible query execution performance with the current server availability.

{:.comment data-author="RT"}
We can only implement the client-part of the cost model on Comunica.
The server-part will have to be implemented as a wrapper on top of existing systems.
And I actually think Comunica doesn't need to be mentioned here, so this paragraph can probably be moved to conclusions.
I suggest to instead mention what we will explain in this paper (the architecture stuff).

In this paper, we plan to implement our double-side (client/server) cost models on top of [Comunica](cite:cites taelman_iswc_2018) which is a flexible query engine platform that is able to query multiple heterogeneous interfaces.
The modular architecture of Comunica supports internal negotiation between different logic paths using *mediators*.
Our proposed client-side cost model will be implemented using such a mediator.
