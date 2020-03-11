## Conclusions

This article outlines our high-level framework.
In future work, we will implement the server and client components,
and evaluate different cost models.

We intend to implement our client component using the [Comunica platform](cite:cites taelman_iswc_2018) as a _Mediator_
that can determine optimal interfaces based on different circumstances.
This will allow us to focus on the cost model aspect of the client,
as Comunica already supports the majority of the intended LDF interfaces and all SPARQL query operators.

Our envisioned cost-model-based framework for enabling query execution over hybrid LDFs
is a key element in achieving the vision of a Web where any client can query data over any combination of heterogeneous interfaces.
Publishers may choose to expose different kinds of interfaces based on different needs,
which may potentially change at runtime, for which a cost model is essential.
