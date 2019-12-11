## Introduction
{:#introduction}

Linked Data (LD) provides standards for publishing (RDF)and (SPARQL) querying Knowledge Graphs on the Web,serving, accessing and processing such open, decentralized datasets is often practically impossible due to query timeouts on publicly available SPARQL endpoints show. Another option is to make the data publicly available as data dumps. In order to query the datadumps, the full dataset needs to be downloaded on the local machine that supports SPARQL query engine.  These could be effective option with very huge SPARQL query workload, but it does not comply to the aim of Semantic Web which allows the live querying.

Alternatively Linked Data Fragments (LDF), introduced the foundation of a framework that distributes the load of the query execution between the clients and the server as well as the financial costs of queries execution among data providers. 

First, LDF laid the basis to define Triple Pattern Fragments (TPF) interface that attempts to tackle the problem of availability through providing intelligent TPF clients  which shifted the complex query processing workload to the client side, but with the cost of the increase of network overhead due to unnecessary transfer of large intermediate results in addition to longer query execution time that lowers the performance.

To address the drawbacks of TPF, Bindings-Restricted Triple Pattern Fragments (brTPF)  is an extended interface of TPF that gives a slight boost to the performance of 	query execution through by attaching intermediate results to triple pattern requests together with distributing the join between the client and the server using the bind join strategy. In this manner, brTPF reduces the number of HTTP requests in addition to minimize the amount of data transferred than the original TPF. However, brTPF still have considerably high HTTP requests besides the shortcoming of the ability to scale with larger datasets. 

Recently, SaGe is a Web preemption based SPARQL query engine designed to avoid the starvation of the simple queries waiting for the complex ones that consume the server resources. SaGe utilized Round-Robin algorithm to maintain a fair allocation of server resources between queries. SaGe formalized a model that enables to suspend and proceed queries with the mechanism to save the state of the query execution. Additionally, SaGe has implemented full mappings operators such as ORDER BY, OPTIONAL as well as aggregation function to be executed on the client-side. Experiments showed that SaGe has enhanced the average completion time per client in addition to reduces the average network traffic per client. However, SaGe extensively consumes the server resources. Besides, the performance of SaGe is degrading with the increasing sizes of the knowledge graphs as well as the execution time of the complex queries is substantially increased.

Finally, smartKG is a novel approach that introduced a new paradigm to distribute the query processing between the client and the server through combining shipping compressed knowledge graph partitions in addition to intermediate results shipped using TPF. The experimental evaluation demonstrated that smartKG outperformed the existing approaches in server resource usage in addition to the average workload execution time as well as less timeout queries. On the other hand, SPARQL endpoints and SaGe has a better performance than smartKG with less number of clients and small-scale knowledge graphs. Although smart-KG has better average workload execution time, TPF and SaGe outperform smartKG in certain types of queries.

The main objective of this research is to provide a more intelligent interface that benefits from the variety of capabilities of the currently existing query engine through introducing double-side (client/server) cost models. Thus the proposed interface will insure that the server does not exceed its processing capabilities while maintaining a high query run time performance.

 
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
