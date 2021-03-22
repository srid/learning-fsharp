https://github.com/DevrexLabs/memstate

> In-memory event-sourced ACID-transactional replicated object graph engine. What? Can you say that again? Ok, it's **an application server that keeps all your data in RAM**. It runs without a database because **all the transactions are recorded in a log and used to restore the state of the application at startup** or when setting up a replica. You define the **object model, commands and queries** using C#. Besides being very simple Memstate is also very fast and will outperform any relational database.

In the Haskell world, a similar tool is [acid-state](https://github.com/acid-state/acid-state).