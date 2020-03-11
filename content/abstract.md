## Abstract
<!-- Context      -->
A multitude of Linked Data Fragments (LDF) server interfaces have been proposed to expose Knowledge Graphs (KGs) on the Web.
Each of them lead to different trade-offs when clients execute queries over them,
such as how query execution effort is distributed between server and client.
There is however no single _silver bullet_ that works best everywhere.
Each of these interfaces have diverse characteristics that very performance in terms of
server effort, client effort, and network bandwidth.
<!-- Need         -->
Currently, publishers can only pick one of these interfaces to expose their KGs on the Web.
However, in some cases, multiple interfaces may be suitable for the publisher,
and these may even vary over time based on the aforementioned factors.
<!-- Task         -->
As such, we propose a hybrid LDF interface that can expose multiple interfaces based on a server-side cost model.
Additionally, we sketch a negotiation protocol through which clients can determine desirable interfaces
during query planning using a client-side cost model.
<!-- Object       -->
In this paper, we lay out the high-level ideas behind this hybrid framework,
and we explain our future steps regarding implementation and evaluation.
<!-- Findings     -->
<!-- Conclusion   -->
<!-- Perspectives -->
As such, our work provides a basis for exploiting the trade-offs that exist
between different LDF interfaces for optimally exposing KGs on the Web.
