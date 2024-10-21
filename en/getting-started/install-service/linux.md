# Linux

## Overview

This page will describe the basic features of the Linux service, how to register and what metrics are collected from the technology.

## Installation

The Linux service is built to be generally compatible with today's most popular operating systems.

### Compatibility

Below is a list of operating systems already 100% integrated.

> If your Distro is not on the list, it does not mean that it will not be compatible, as the service works in a generic way. If your Distro is based on one of the list, you can install without adversity

| Distro             | Compatibility |
| ------------------ | ------------- |
| Amazon Linux       | >=2022        |
| CentOS             | >= 6 (2011)   |
| Debian             | >= 9 (2017)   |
| Fedora             | >= 37         |
| Red Hat Enterprise | >= 7          |
| Ubuntu             | >= 18.04      |

### Prerequisites

To register for the service, you must meet certain prerequisites.

- User create on host for Agent used
- SSH server installed on host
- RSAAuthentication and PubkeyAuthentication enabled on it
- Key pair (Public Key and Private Key) generate for Agent User

## Quick Deploy

This is a quick guide for installing the Linux service on the dbsnOOp Platform

![GUIDeployLinux](https://opendocs.dbsnoop.com/deploylinuxgui.jpg)

1. Within the platform, access the Deploy panel and select the Linux service. After, on the registration screen, select the used Agent to connect to service

> The selected agent must be on the same network as the service to be registered!

1. Access the “Credentials” tab to change the agent username that was previously created and the private key created for him.

> If a user and keys have not been created, the one-line command can be used to perform this step within the host
> Exemple:
>
> ```none
> API_KEY="<DBSNOOP_API_KEY>" bash -c "$(curl -kfsSL <DBSNOOP_API_URI>/services_monitored/linux/installation)"
> ```
>
> Copy

1. Define the host and port used for access via SSH
2. It is necessary to test the connection before finalizing.
3. After testing, the service can be registered!

> The waiting time for display in the system and the start of metrics collection may vary according to the delay in the network!

## Metrics

Below is the list of metrics that the Agent collects from the service for use within the platform

| Metric              | Resource | Description |
| ------------------- | -------- | ----------- |
| cpu_usage           | System   |             |
| lan_connection      | Network  |             |
| load                | System   |             |
| swap_usage          | Memory   |             |
| connected_users     | Network  |             |
| waiting_connections | Network  |             |
| disk_space          | Disk     |             |
| memory_usage        | Memory   |             |
| system_info         | System   |             |
| system_stats        | System   |             |
| network_usage       | Network  |             |
| cpu_stats           | System   |             |
| tcp_udp_stats       | Network  |             |
| memory_stats        | System   |             |
| system_blocks       | Disk     |             |
| disk_stats          | Disk     |             |
| environment         | System   |             |