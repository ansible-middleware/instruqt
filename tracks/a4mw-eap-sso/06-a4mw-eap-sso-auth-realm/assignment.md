---
slug: a4mw-eap-sso-auth-realm
id: rrqhy3aunpvs
type: challenge
title: Configuring Single Sign-On
teaser: Use the redhat.sso collection sso_realm role to fully configure an authentication
  realm
notes:
- type: text
  contents: Replace this text with your own text
tabs:
- title: Automation controller
  type: service
  hostname: control
  path: /
  port: 443
- title: Terminal
  type: terminal
  hostname: control
- title: editor
  type: service
  hostname: control
  path: /editor/
  port: 443
difficulty: basic
timelimit: 600
---
---
 💡 Auth realm and EAP subsystem
===
#### Estimated time to complete: *20 minutes*<p>


☑️ Task 1 - Load the repository directory in the editor
===

1. Go to the **editor** tab, clicking on the link in topbar; if the git repository is still open from the previous challenge, proceed to Task 2 below.
2. In the **editor** tab, click on the File menu, then **Load directory**
3. Select the **eap-sso** directory, which is the working copy of the git repository
4. Click **OK** and then confirm in the dialog that open, that you trust the contents


☑️ Task 2 - Create a realm playbook
===

☑️ Task 3 - Configure the EAP keycloak subsystem
===


✅ Next Challenge
===
Press the `Check` button below to go to the next challenge once you’ve completed the task.

🐛 Encountered an issue?
====

If you have encountered an issue or have noticed something not quite right, please [open an issue](https://github.com/ansible-middleware/instruqt/issues/new?labels=a4mw-eap-sso&title=Issue+with+Deploy+Red+Hat+Single+Sign-On+with+Ansible+for+Middleware+collections+slug+ID:+a4mw-eap-sso-auth-realm&assignees=guidograzioli).

<style type="text/css" rel="stylesheet">
  .lightbox {
    display: none;
    position: fixed;
    justify-content: center;
    align-items: center;
    z-index: 999;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    padding: 1rem;
    background: rgba(0, 0, 0, 0.8);
    margin-left: auto;
    margin-right: auto;
    margin-top: auto;
    margin-bottom: auto;
  }
  .lightbox:target {
    display: flex;
  }
  .lightbox img {
    /* max-height: 100% */
    max-width: 60%;
    max-height: 60%;
  }
  img {
    display: block;
    margin-left: auto;
    margin-right: auto;
  }
  h1 {
    font-size: 18px;
  }
    h2 {
    font-size: 16px;
    font-weight: 600
  }
    h3 {
    font-size: 14px;
    font-weight: 600
  }
  p span {
    font-size: 14px;
  }
  ul li span {
    font-size: 14px
  }
</style>
