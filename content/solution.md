## Solution
{:#solution}

The goal of our proposed framework
is to allow servers to expose different kinds of interfaces
based on the current server load and the used SPARQL queries.
Instead of making the server allow *just one interface* type per query,
we propose allowing a *collection of interfaces* to be exposed per query.
This allows the client to select the most desired interface
based on the clients capabilities and circumstances.

To achieve such a hybrid of server interfaces,
we make use of a server-side cost model for selecting a set of interfaces based on a given query,
and a client-side cost model for determining a query execution plan based on the allowed interfaces.
[](#figure-solution) shows an overview of this framework
where client-side query engines start by sending a query `q` to the server,
and receive an answer that contains a token `t` and a set of allowed interfaces `I`.
Based on the returned interfaces,
the client can determine a query decomposition over these interfaces.
These (sub)queries can then be resolved by requesting the appropriate interfaces using the given token.
Hereafter, we explain the server and client processes in more detail.

<figure id="figure-solution">
<img src="img/hybrid-querying.svg" alt="[Hybrid Linked Data Fragments]">
<figcaption markdown="block">
Overview of client-server communication for a cost-model-based query execution over a hybrid of Linked Data Fragments interfaces.
</figcaption>
</figure>

### Server Component

params
{:.todo}

### Client Component

params
{:.todo}

Also mention clients combining different interfaces at the same time (e.g. tpf + smartkg)
{:.todo}
