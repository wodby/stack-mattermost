# Mattermost application stack for Kubernetes on Wodby

Deploy Mattermost Team Edition on Kubernetes with Wodby.

This repository defines the Wodby stack manifest and its default service
composition.

<!-- wodby:generated:start -->

## Stack contract

- [Mattermost stack on Wodby](https://wodby.com/stacks/mattermost)
- [Browse Wodby application stacks](https://wodby.com/stacks)
- [Wodby stack documentation](https://wodby.com/docs/2.0/stacks/)
- [Stack manifest reference](https://wodby.com/docs/2.0/stacks/template/)

## Service definitions

- [Mattermost service](https://github.com/wodby/service-mattermost)
- [PostgreSQL service](https://github.com/wodby/service-postgres)
- [OpenSMTPD service](https://github.com/wodby/service-opensmtpd)

## What's included

| Component / service | Default configuration |
| --- | --- |
| Mattermost<br>`mattermost` | required; enabled by default; links: `postgres` → `postgres`, `sendmail` → `opensmtpd` |
| PostgreSQL<br>`postgres` | required; enabled by default; volumes: `data` 20 GB |
| OpenSMTPD<br>`opensmtpd` | optional; enabled by default |

Enabled optional services are selected by default but can be excluded when an
app is created. Disabled optional services are available but not selected by
default. Required services cannot be excluded.

## Validate the stack manifest

```bash
wodby stack validate-manifest stack.yml --org <org-id>
```

<!-- wodby:generated:end -->

## Operational scope

This stack is intended for simple, single-replica Mattermost installations.
The Mattermost service uses local persistent storage and must run on a
`linux/amd64` node.

Mattermost Calls is disabled because supported Kubernetes deployments require
a dedicated RTCD service and direct TCP/UDP media routing. Highly available
deployments also require shared file storage and a broader service topology.

## Deploy this stack

Review the service version, volume sizes, SMTP requirements, and cluster
architecture when creating the application. Back up the PostgreSQL database
and the Mattermost volume as one consistent recovery set.

## Maintain a custom version

1. Fork this repository.
2. Edit `stack.yml`.
3. Import the repository as a [Git-backed stack](https://wodby.com/docs/2.0/stacks/create/#create-a-git-backed-stack).

When replacing or renaming a stack service, update every related link target.
Stack-local names and referenced service names are distinct identifiers.
