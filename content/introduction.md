## Introduction
{:#introduction}
The rapid growth of open and decentralized Knowledge Graphs over the Web has created an immense demand for public Knowledge Graph query services.
However, serving live queryable Knowledge Graphs on the Web is difficult
due to the [low availability](cite:cites verborgh_jws_2016)
and expensive hosting of SPARQL endpoints.
As an alternative, publishing data dumps moves query effort to the client, but this may not always be desirable.
Recently, the [Linked Data Fragments (LDF)](cite:cites verborgh_jws_2016) framework was introduced
to explore the range of Web query interfaces that exist between SPARQL endpoints and data dumps that distribute query execution load between clients and servers.

Several approaches have emerged following this framework such as [Triple Pattern Fragments (TPF)](cite:cites verborgh_jws_2016) and [Bindings-Restricted TPF (brTPF)](cite:cites brTPF), [SaGe](cite:cites minier2019sage) and [smart-KG](cite:cites smartKG), each offering their own trade-offs. For instance, TPF and brTPF increase server availability at the cost of increased network load. SaGe enhances average query performance at the cost of increased server load for concurrent complex queries. smart-KG increases server availability at the cost of higher client effort. Research shows that no single optimal approach exists,
but they all have their advantages and disadvantages. As such, there is a need for a hybrid LDF approach that determines one or more efficient query approaches based on changing circumstances.

A [preliminary hybrid LDF approach](cite:cites hetero) investigated the diversity of [LDF characteristics](cite:cites Montoya2019AnalysisOT) that can influence query execution plans.
[Another proposal](cite:cites khanISWC2019) provides a different interface based on the current server workload.
None of the aforementioned hybrid approaches allow clients and the server to negotiate query interfaces depending on factors such as the executed query, server load, client capabilities, and network bandwidth. In this paper, we propose a negotiation-based hybrid. Using a server-side cost model, the server can expose one or more query interfaces based on its current load, and the query that the client aims to execute. Using a client-side cost model, an efficient query plan over the available interfaces can be determined.
This combination of server and client cost model ensure efficient usage of server and client resources
to aim for the best possible query performance over the available LDF approaches.
