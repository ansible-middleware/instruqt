---
slug: wildfly
id: dafan33segmq
type: challenge
title: Setting up the RHEL 8 machine
tabs:
- title: getting_started
  type: terminal
  hostname: getting-started-demo
  workdir: /home/getting_started/
difficulty: basic
timelimit: 600
---
👋 Introduction to Ansible Middleware
===

Getting up to speed with Ansible Middleware is easy and only requires a few steps. This tutorial demonstrates and guides you through the process of preparing a local machine with the necessary tooling and then deploying an instance of Wildfly using the Wildfly collection provided by Ansible Middleware.

For this tutorial, we are using an Execution Environment and the ansible-navigator utility to perform the automation and provisioning of the Wildfly instance. Install and configure ansible-navigator based on the documentation for your target operating system. To perform the execution of the automation, the ansible-middleware-ee Execution Environment provided by the Ansible Middleware team includes all of the Ansible Middleware collections and their dependencies, so there is no need to install any additional components on the control node. We would be using our execution environment as it already includes all of our latest collections so we don’t have to set it up again.

Once the virtual machine is up and running, let's now check the version of RHEL its on using the following command:

```
cat /etc/redhat-release
```

☑️ Task 1 - Prepare the environment
===

Install ansible:

```
python3 -m pip install --user ansible
```

Install ansible-navigator:

```
python3 -m pip install ansible-navigator --user
```

☑️ Task 2 - Explore the Ansible Middleware EE
===

Once ansible-navigator has been installed, execute the following command to browse all of the collections that are included within the Execution Environment Image:

```
ansible-navigator --eei quay.io/ansible-middleware/ansible-middleware-ee:latest collections
```

✅ Next Challenge
===
Press the `Next` button below to go to the next challenge once you’ve completed the tasks.

🐛 Encountered an issue?
====

If you have encountered an issue or have noticed something not quite right, please [open an issue](https://github.com/ansible-middleware/instruqt/issues/new?labels=getting-started-with-ansible-middleware&title=Issue+with+Getting+started+with+Ansible+Middleware+slug+ID:+wildfly&assignees=hcherukuri).
