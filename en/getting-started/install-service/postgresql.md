# PostgreSQL
## Overview

This page will describe the basic features of the **PostgreSQL** service, how to register and what metrics are collected from the technology.

## Installation

The **PostgreSQL** service is built to be generally compatible with today's most popular operating systems.

### Compatibility

Below is a list of **PostgreSQL** Versions already 100% integrated.

| Version    | Compatibility |
| ---------- | ------------- |
| PostgreSQL | >= 9          |

### Prerequisites

To register for the service, you must meet certain prerequisites.

- User create on database for Agent used

For **PostgreSQL** Version >= 10:

```sql
CREATE USER <DBSNOOP_AGENT_USER> WITH PASSWORD '<PASSWORD>';
GRANT pg_monitor TO <DBSNOOP_AGENT_USER>;
GRANT SELECT ON pg_stat_database TO <DBSNOOP_AGENT_USER>;
```

For an older **PostgreSQL** version:

```sql
CREATE USER <DBSNOOP_AGENT_USER> WITH PASSWORD '<PASSWORD>';
GRANT SELECT ON pg_stat_database TO <DBSNOOP_AGENT_USER>;
```

If you're running **PostgreSQL** version <=9.6, you need to create a SECURITY DEFINER to read from pg_stat_activity:

```sql
CREATE FUNCTION pg_stat_activity() RETURNS SETOF pg_catalog.pg_stat_activity AS
$$ SELECT * from pg_catalog.pg_stat_activity; $$
LANGUAGE sql VOLATILE SECURITY DEFINER;
```

## Quick Deploy

This is a quick guide for installing the **PostgreSQL** service on the dbsnOOp Platform

1. Within the platform, access the Deploy panel and select the **PostgreSQL** service. After, on the registration screen, select the used Agent to connect to service

{% hint style="info" %}

The selected agent must be on the same network as the service to be registered!

{% endhint %}

1. Access the “Credentials” tab to change the agent username that was previously created and the password created for him.
2. Define the host and port used for database access. Default 5432
3. It is necessary to test the connection before finalizing.
4. After testing, the service can be registered!

{% hint style="info" %}

The waiting time for display in the system and the start of metrics collection may vary according to the delay in the network!

{% endhint %}

# Metrics

Below is the list of metrics that the Agent collects from the service for use within the platform

| Metric                 | Resource    | Description |
| ---------------------- | ----------- | ----------- |
| processlist            | Threads     |             |
| locks                  | Threads     |             |
| status                 | Avaiability |             |
| pg_watch               | System      |             |
| network_traffic        | System      |             |
| index_statistics       | Structure   |             |
| query_statistics       | Threads     |             |
| db_info                | Avaiability |             |
| query_cache_statistics | Threads     |             |
| autovacuum_statistics  | Avaiability |             |
| db_status              | Avaiability |             |
| second_plan            | Avaiability |             |
| configuration          | System      |             |
| user_audit             | Audit       |             |
| auto_increment         | Structure   |             |
| table_stats            | Structure   |             |
| cache_hit_rate         | Avaiability |             |

