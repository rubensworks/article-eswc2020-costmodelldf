## Hybrid Framework
{:#solution}
{:.todo Tokens should be assembled with an expiry date}
{:.todo Enlarge the figure, add parenthesis}
{:.todo What do you mean by query complexity? predict execution time?}
{:.todo Should we define a function for the cost model (Mathmatical formulation)?}
{:.todo What type of cost model?threshold-based?then we need a policy (selection function based on these values)?}
{:.todo For the algorithm, should we use getThreshould and getValue(metric)? better Naming?}
{:.todo define continous effciency?}
{:.todo Notneeded sentence "even if a SPARQL endpoint was allowed ...." }
The goal of our proposed framework
is to allow servers to expose different kinds of interfaces
based on the current server load and the used SPARQL queries.
Instead of making the server allow *just one interface* type per query,
we propose allowing a *collection of interfaces* to be exposed per query.
This allows the client to select the most desirable interface
based on the clients capabilities, query plans, and other circumstances.

To achieve such a hybrid of server interfaces,
we make use of a server-side cost model for selecting a set of interfaces based on a given query,
and a client-side cost model for determining a query execution plan based on the allowed interfaces.
[](#figure-solution) shows an overview of this framework
where client-side query engines start by sending a query `q` to the server,
and receive an answer that contains a token `t` and a set of allowed interfaces `I`.
Based on the returned interfaces,
the client can determine a query plan over these interfaces.
These (sub)queries can then be resolved by requesting the appropriate interfaces using the given token.
Hereafter, we explain the server and client in more detail.

<figure id="figure-solution">
<img src="img/hybrid-querying.svg" alt="[Hybrid Linked Data Fragments]" style="height: 8em">
<figcaption markdown="block">
Overview of client-server communication for a cost-model-based query execution over a hybrid of Linked Data Fragments interfaces.
</figcaption>
</figure>

### Server Component

The server component of our framework consists of
a cost model for calculating a set of allow interfaces,
and a token-based wrapper over a set of interfaces.
We explain these two elements hereafter.

#### Cost Model

The goal of this server-side cost model is to ensure the server availability,
and to allow queries to be executed as fast as possible.
Since the latter goal can sometimes be detrimental to the server availability,
for example when many concurrent users are sending highly complex queries,
the availability goal must always have priority in the model.

Based on these goals, the model should be able to make a suggestion for a set of interfaces
based on a given query and a set of internal metrics.
For this, we propose a set of internal metrics such as the current CPU usage, memory usage and network I/O.
The server administrator must be able to configure a threshold for these metrics,
so that the cost model can select interfaces that optimize both goals.

[](#algorithm-get-allowed-interfaces) shows the pseudocode of an algorithm
that can be used to calculate a set of allowed interfaces.
In this algorithm, `CalculateMetricIncrease` would still need a concrete implementation.
For this, different possibilities exist,
such as heuristics to predict query complexity based on the number of triple patterns and query operators.
<!--For each incoming query `q`,
the algorithm iterates over all available interfaces, and all metrics.
For each metric, the expected metric value increase is calculated
for the given query using `CalculateMetricIncrease(q, metric)`.
If when adding this value to the current metric's value does not exceed the maximum allowed metric value,
then the loop continues.
If all metrics pass for a given interface,
then an interface is considered an *allowed interface*.-->

<figure id="algorithm-get-allowed-interfaces" class="listing">
````/code/get-allowed-interfaces.txt````
<figcaption markdown="block">
Algorithm for calculating the allowed interfaces for a given query.
</figcaption>
</figure>

<!--Based on our algorithm, the `CalculateMetricIncrease` still needs a concrete implementation.
For this, different possibilities exist.
For instance, heuristics for query complexity can be used to estimate metric value increases,
such as query string length, the depth of the basic graph patterns or the used query operators.
Furthermore, other implementations may be based on query log analysis,
where models could be based on machine learning techniques.-->

#### Interface Wrapper

Based on the server-side cost model,
the server can wrap over a number of LDF interfaces
that the publisher wants to expose.
This wrapper is a proxy that accepts SPARQL queries,
and replies with a token and a set of allowed interfaces
that have been calculated for the given query using the server-side cost model.
The token is *required* for performing any requests to any of the wrapped LDF interfaces.

This token should be seen as temporary *permission*
to make use of a specific set of query capabilities from the data publisher.
It is important that the server validates this token upon every request to an LDF interface.
If the server would not do this,
a client could simply ignore the set of allowed interfaces,
and always execute queries against the most expressive interface (e.g. SPARQL endpoint),
even if this interface was not allowed by the server.

<!--Optionally, the server could keep track of token usages
to check whether or not the client does indeed use it
to execute the query it got permission for, and nothing more.
Since keeping track of this token usage could require significant server effort,
simpler heuristics could be used,
such as limiting the temporal validity of a token to the estimated execution time.-->

<!--An optional enhancement of the server could be to directly
reply with a SPARQL query response
if the only allowed server was a SPARQL endpoint,
because the client will be likely to make such a subsequent request.-->

### Client Component

In most cases, the primary goal of clients is to execute queries as fast as possible,
either in overal execution time,
or in continuous efficiency.
There could however be a number of metrics that can soften this need for fast query execution,
such as reducing CPU or bandwidth usage, or [optimizing for early results](cite:cites diefficiency)

Using the server-side hybrid of LDF interfaces that was explained before,
clients will retrieve a set of allowed interfaces based on a given query.
Based on these interfaces, the client should determine a query plan that makes use of the interfaces
in such a way that is as efficient as possible with respect to the client's metrics.
While most client-side query algorithms focus on splitting up queries for execution against a single type of interface,
additional algorithms are needed for [*intelligently combining interfaces* for certain subqueries](cite:cites hetero).

Next to these client metrics, there could be additional parameters that could influence
the selection of interfaces to query from.
For example, if the client knows beforehand that it will have to execute *many* queries against the same dataset,
then it might be more efficient to download the full dump of the dataset,
even if a SPARQL endpoint was allowed for the initial query.
Another case that can influence interface selection
would be when certain partial dumps of the dataset are already available locally,
or [within a network of peers](cite:cites webp2p).
