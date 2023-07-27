# PostgreSQL HA

PostgreSQL is a powerful, open source object-relational database system with over 35 years of active development that has earned it a strong reputation for reliability, feature robustness, and performance. We're using **PostgreSQL Containers packaged by Bitnami** and [here's why](https://github.com/bitnami/containers/tree/main/bitnami/postgresql-repmgr#why-use-bitnami-images).

The manifests defined here deploys a PostgreSQL Database Server With High Availability Using Kubernetes Statefulsets.

## What does High Availability means for Postgresql?

High Availability (HA) in the context of PostgreSQL refers to designing a fault-tolerant and resilient database system that can maintain data availability and serve queries even during various failure scenarios. The primary objective is to eliminate single points of failure and introduce redundancy measures to ensure continuous access to data.


## High Level Architecture

The PostgreSQL HA cluster setup deploys a master-slave topology. The master node has writing permissions while replication is on the slaves nodes which have reading-only permissions.

![Image Not Available](<postgresql-ha-architecture.png>)

To achieve high availability for PostgreSQL, the following two components are crucial:

- `Replication Manager`: an open-source tool for managing replication and failover on PostgreSQL clusters. This module ensures high-availability thanks to automatic membership control. If the master is down, any of the slave nodes will be promoted as master to avoid data loss.
  
- `Pgpool-II`: the PostgreSQL proxy. It stands between PostgreSQL servers and their clients providing connection pooling and load balancing to spread the queries among nodes.

The failover mechanism provided by RepMgr and the Load balancing provided by Pg-pool ensure that the Postgres cluster remains up for a long time. The two mechanisms together ensure the high availability of the PostgreSQL cluster.

## Convert Helm Chart to Kubernetes YAML

Converting a Helm chart to kubernetes YAML is very easy. In helm, there is a command called `helm template`. Using the template command you can convert any helm chart to a YAML manifest. Ensure that you have helm installed to execute the command.

The syntax for using helm template is as follows:

```bash
helm template <release_name> <chart_name> [flags]
```

- `<release_name>`: The name to assign to the release (optional).
- `<chart_name>`: The name of the Helm chart to be templated.

Flags can be used to customize the rendering process. Some common flags include:

- `--set`: Allows you to override chart values directly from the command line.
- `--values`: Specifies one or more YAML files with custom values for the chart.
- `--output-dir`: Specifies a directory to store the rendered Kubernetes manifest files.

The resultant manifest file will have all the default values set in the `values.yaml`. However, you can use the `--set` flag with the helm template command to override specific values directly from the command line. For example:

```bash
helm template <release_name> <chart_name> --set key1=value1,key2=value2,...
```

Now, lets list down the steps required to generate the kubernetes manifest using the [Bitnami's Helm Chart for PostgreSQL HA](https://github.com/bitnami/charts/tree/main/bitnami/postgresql-ha).

- **Step 1:** Add Helm Repository

  ```bash
  helm repo add bitnami https://charts.bitnami.com/bitnami
  ```

- **Step 2:** After you have added the repository, update your local repositories.

  ```bash
  helm repo update
  ```

- **Step 3:** Convert the Bitnami PostgreSQL HA Helm chart to kubernetes YAML

  ```bash
  helm template postgresql-ha bitnami/postgresql-ha --set postgresql.image.tag=12.15.0-debian-11-r65  --output-dir=.
  ```

The resultant manifest files will get generated in the specified output directory. For full list of available parameters and their default values, [click here](https://github.com/bitnami/charts/tree/main/bitnami/postgresql-ha#parameters).


