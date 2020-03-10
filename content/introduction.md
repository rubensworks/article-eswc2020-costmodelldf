## Introduction
{:#introduction}
The rapid growth of open and decentralized Knowledge Graphs over the Web has created an immense demand for public Knowledge Graph query services.
However, serving live queryable Knowledge Graphs on the Web is difficult due to their [low availability](cite:cites verborgh_jws_2016)
and expensive hosting of SPARQL endpoints due to their expressive query capabilities.
As an alternative, by publishing data dumps and requiring clients to query over them client-side, this query effort can be fully pushed to the client, which may not always be desirable either.
Recently, [Linked Data Fragments framework (LDF)](cite:cites verborgh_jws_2016) was introduced as an idea of exploring range
of potential Web querying interfaces that exist between SPARQL endpoints and data dumps.
LDF aims at investigating the trade-offs of the range of solutions that distribute the load of query execution between client and server.

Several approaches have emerged following this LDF framework such as [Triple Pattern Fragments (TPF)](cite:cites verborgh_jws_2016) and [Bindings-Restricted TPF (brTPF)](cite:cites brTPF), [SaGe](cite:cites minier2019sage) and [smart-KG](cite:cites smartKG), each offering their own trade-off between the server availability and the query performance. For instance, TPF and brTPF increase server availability at the cost of increased network load. While SaGe enhances average query performance at the cost of reduced server performance when multiple complex queries are running on the server simultaneously. Finally, smart-KG ensures a higher server availability at the cost of higher client effort.

The research sparked by LDF has shown that no single optimal approach exists.
Instead, they all have their advantages and disadvantages on a varying spectrum.
As such, there is a need for a hybrid LDF approach that determines one or more optimal query approaches based on dynamically changing.

A [preliminary hybrid LDF approach](cite:cites hetero) investigated the diversity of [LDF characteristics](cite:cites Montoya2019AnalysisOT,inbook)
that can influence query execution plans.
[Another proposal](cite:cites khanISWC2019) suggests a server that provides a different query service based on the current server workload.
None of these approaches allow query interfaces to be negotiated between client and server
depending on factors such as the executed query, server effort, client capabilities, and network bandwidth in combination.

In this paper, we propose such a negotiation-based cost-model.
On the one hand, using a server-side cost model,
the server can expose one or more query interfaces based on its current load,
and the query that the client aims to execute.
On the other hand, the client has a cost-based query optimizer that can determine an efficient query plan over the available interfaces.
This combination of server-side and client-side cost model can ensure efficient usage of server and client resources
to aim for the best possible query performance over the available LDF approaches.
