# PostgreSQL Client

We will use the PostgreSQL client to connect & verify the cluster. You can connect to the cluster by following the below steps:-

- Login to the OpenShift cluster
- Extract the postgresql password from the secret
  
    ```bash
    oc get secret postgresql-ha  -o jsonpath="{.data.password}" | base64 --decode
    ```

- Exec into the pg-client pod
  
    ```bash
    oc exec -it pg-client -- /bin/bash
    ```

- Connect to the cluster using the password and pg-pool service
  
    ```bash
    PGPASSWORD=<password> psql -h postgresql-ha-pgpool -p 5432 -U postgres
    ```

## Verifying the PostgreSQL Replication

To verify if the replication is taking place, run the below command after connecting to the cluster using psql client:-
  
```bash
select * from pg_stat_replication;
```

No. of entries you should see = No. of replicas of Postgres running minus 1.

Reason for **“minus 1”**: Data is being replicated from the master to the follower. It’s logically impossible for the Data to be replicated from the master to itself!

## Verify the failover

Verify the failover by deleting the pods randomly and seeing if the cluster becomes unresponsive or not. Sample logs of follower pod when the primary pod goes down: Note how the messages inform the user about a failover taking place!

```bash
NOTICE: promoting standby to primary
DETAIL: promoting server "postgres-sts-1" (ID: 1001) using "/opt/bitnami/postgresql/bin/pg_ctl -o "--config-file="/opt/bitnami/postgresql/conf/postgresql.conf" --external_pid_file="/opt/bitnami/postgresql/tmp/postgresql.pid" --hba_file="/opt/bitnami/postgresql/conf/pg_hba.conf"" -w -D '/bitnami/postgresql/data' promote"
2021-07-28 20:38:11.362 GMT [266] LOG:  received promote request
2021-07-28 20:38:11.370 GMT [266] LOG:  redo done at 0/8000028
2021-07-28 20:38:11.370 GMT [266] LOG:  last completed transaction was at log time 2021-07-28 20:36:57.642182+00
2021-07-28 20:38:11.698 GMT [266] LOG:  selected new timeline ID: 2
2021-07-28 20:38:12.494 GMT [266] LOG:  archive recovery complete
NOTICE: waiting up to 60 seconds (parameter "promote_check_timeout") for promotion to complete
DEBUG: get_recovery_type(): SELECT pg_catalog.pg_is_in_recovery()
INFO: standby promoted to primary after 0 second(s)
DEBUG: setting node 1001 as primary and marking existing primary as failed
DEBUG: begin_transaction()
DEBUG: commit_transaction()
2021-07-28 20:38:13.105 GMT [264] LOG:  database system is ready to accept connections
NOTICE: STANDBY PROMOTE successful
```
