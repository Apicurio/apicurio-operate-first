# PostgreSQL HA

[RepMgr](https://repmgr.org/) is an open-source tool shipped with Postgres which serves the below two purposes:

- **Replication:** It replicates data from the primary server to all the replicas. This helps in reducing the load on the servers by distributing read & write queries.
  
- **Failover:** It can handle failovers in the cluster i.e. it can promote a read-only server to a primary server when required.

This PostgreSQL cluster solution is packaged by Bitnami, and it includes the PostgreSQL replication manager. You can find the full list of available configuration options and their default values [here](https://github.com/bitnami/containers/tree/main/bitnami/postgresql-repmgr#setting-up-a-ha-postgresql-cluster-with-streaming-replication-and-repmgr). However, let’s go through the important env vars for repmgr setup:-

- **REPMGR_PARTNER_NODES:** This expects a comma-separated list of all Postgres server addresses in the cluster. Including the primary server’s address.
  
- **REPMGR_PRIMARY_HOST:** This expects the Postgres primary server’s address.
  
- **REPMGR_USERNAME:** User to be created for the repmgr operations.

- **REPMGR_PASSWORD:** Password to be created for the repmgr operations.

- **REPMGR_DATABASE:** Database to be created for the repmgr operations.