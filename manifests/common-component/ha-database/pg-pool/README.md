# Pgpool-II

[Pgpool-II](https://www.pgpool.net/docs/latest/en/html/index.html) is a middleware component that sits in front of the Postgres servers and acts as a gatekeeper to the cluster.It mainly serves the below two purposes:-

- **Load Balancing:** Pg pool takes connection requests and queries. It analyzes the query to decide where the query should be sent.Read-only queries can be handled by read-replicas. Write operations can only be handled by the primary server. In this way, it loads balances the cluster.

- **Limits the requests:** Like any other system, Postgres has a limit on no. of concurrent connections it can handle gracefully.Pg-pool limits the no. of connections it takes up and queues up the remaining. Thus, gracefully handling the overload.

This Pgpool container is packaged by Bitnami. You can find the default and available configuration options [here](https://github.com/bitnami/containers/tree/main/bitnami/pgpool#environment-variables).
