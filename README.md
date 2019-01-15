# An Ansible role to setup and configure the HAProxy integration for the Datadog Agent
The Datadog.datadog role maintained by Datadog is great, but it does not attempt to configure
monitored services for monitoring, and in order to have it configure multiple integrations, you
would either have to duplicate your configs a lot, or do tricky things with Ansible variables
which you shouldn't be doing and aren't worth your time.

This role provides an alternate way to setup a target machine and its Datadog agent to monitor
HAProxy.

## Installation

It is strongly recommended that the [Datadog.datadog role][] is used to install the agent.

This integration requires HAProxy be configured to expose a stats endpoint over http. The datadog
integration's configuration provided in the role's defaults will work with a block such as
```
listen stats # Define a listen section called "stats"
    bind :9000 # Listen on localhost:9000
    mode http
    stats enable  # Enable stats page
    stats hide-version  # Hide HAProxy version
    stats realm Haproxy\ Statistics  # Title text for popup window
    stats uri /haproxy_stats  # Stats URI
    stats auth datadog:changeme  # Authentication credentials
```
although the password should very much be changed.

Consult this role's [defaults](defaults/main.yml) for variables names.

[Datadog.datadog role]: https://github.com/DataDog/ansible-datadog
