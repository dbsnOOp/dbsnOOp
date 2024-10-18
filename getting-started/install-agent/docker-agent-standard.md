---
description: >-
  This guide provides an introduction to using the Agent and how it is used to
  send metrics for services and instances registered on the dbsnOOp platform.
---

# Docker Agent

***

## Overhead

General consumption varies according to the number of services coupled to it. On average, a service has an expected consumption of 0.05% of CPU on average and 150 Kb of RAM.

***

## Installation <a href="#installation" id="installation"></a>

### Variables <a href="#deploy" id="deploy"></a>

| Variable           | Type     | Description                                                                                   |
| ------------------ | -------- | --------------------------------------------------------------------------------------------- |
| SNOOP\_API         | Required | dbsnOOp API URL, used as a communication channel for the platform and sending service metrics |
| SNOOP\_KEY         | Required | Unique key used to register the agent                                                         |
| SNOOP\_AGENT\_NAME | Optional | Customized name for identifying the agent within the platform                                 |



### Deployment

Within the dbsnOOp platform, we have a session dedicated to Deploys to speed up this process. In the deployments panel, we will access the Agent screen and select the model or system on which we will perform this installation.

Each model or system may require specific steps, but this entire process is described within its own installation page, and a one-line command is provided to make things easier.

Exemple Docker one-line install command:

```
docker run -d --name dbsnoop_agent --restart always -e "SNOOP_API=<DBSNOOP_API>" -e "SNOOP_KEY=<DBSNOOP_AGENT_KEY>" -e "SNOOP_AGENT_NAME=<AGENT_NAME>" dbsnoop/agent
```

dbsnOOp Agent has now been installed. You can check to see whether the Agent container has started by running `docker ps`:

```
root@server:~# docker ps
CONTAINER ID   IMAGE                          COMMAND                  CREATED           STATUS          PORTS    NAMES             
06f80b012969   dbsnoop/agent                  "docker-php-entrypoi…"   20 seconds ago    UP 20 seconds            dbsnoop_agent
```

To verify the agent status by running `dbsnoop stats` in container or by `docker exec -t`:

```
root@server:~# docker exec -t dbsnoop_agent dbsnoop stats
dbsnOOp Agent (v1.5.5)
API - Connected
Tasks...
Uptime - 2022-01-19 02:18:12 (188s)
Last Execution - 2022-01-19 02:21:17 (Unix - 1718763677)
Task per Sec - 0.9
Services - 2 (Executions 178)
mysql - 77 - (Executions 102)
linux - 46 - (Executions 76)
```

## Troubleshooting <a href="#troubleshooting" id="troubleshooting"></a>

### Container keeps restarting/dbsnOOp doesn't identify the agent <a href="#issue001" id="issue001"></a>

***Warning!** All examples shown below use the default container name our setup wizard gives, which is **dbsnoop_agent**. If you changed your container name in the installation, please alter the following steps using your defined container name.*

If you try to install the agent via docker and either the container keeps restarting, or dbsnOOp doesn't identify the new agent, it could be an issue with docker permissions. You can identify that with the following code:

```
root@server:~# docker logs dbsnoop_agent
[...]
00:00:06 INFO      [Agent] Validating Agent Configuration
00:00:06 INFO      [Agent] Registering Agent
00:00:06 ERROR     [Agent] cURL error 6: getaddrinfo() thread failed to start (see https://curl.haxx.se/libcurl/c/libcurl-errors.html) for https://poo
[...]
```

Another way you can diagnose this error is through our own stats script, as appointed above. The output should be similar to this:

```
Error response from daemon: Container <container_id> is restarting, wait until the container is running
```

In this case, you can try to remove the container, and add the `--security-opt seccomp=unconfined` flag to raise the permissions granted to the container. This flag should be add right after the container name, and before the `--restart always` flag, as shown below:

```
docker run -d --name dbsnoop_agent --security-opt seccomp=unconfined --restart always -e "SNOOP_API=<DBSNOOP_API>" -e "SNOOP_KEY=<DBSNOOP_AGENT_KEY>" -e "SNOOP_AGENT_NAME=<AGENT_NAME>" dbsnoop/agent
```

You will need to stop and remove the container before recreating it, which you can do with the following command:

```
docker stop dbsnoop_agent && docker rm dbsnoop_agent
```

