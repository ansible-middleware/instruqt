---
slug: playbook
id: mtxbklqxymzx
type: challenge
title: Deploy the playbook
tabs:
- title: getting_started
  type: terminal
  hostname: getting-started-demo
  workdir: /home/getting_started/
difficulty: basic
timelimit: 600
---
Now, run the playbook using ansible-navigator and the execution environment to configure wildfly on the remote node.

```
ansible-navigator --eei quay.io/ansible-middleware/ansible-middleware-ee:latest run wildfly.yml -m stdout --become
```
