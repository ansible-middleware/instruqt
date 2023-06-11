---
slug: a4mw-eap-sso-collections
id: jabxfy1rqlke
type: challenge
title: Collections to the rescue
teaser: Import the Red Hat SSO collection and deploy an HA cluster
notes:
- type: text
  contents: |-
    # Ansible for Middleware collections

    Our latest deployment left us with a non-functional application. We already used the Red Hat EAP and JBCS collections, let's see if we can
    find something else that can help us:

    ![hub-collections.png](../assets/hub-collections.png)

    .
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
- title: JBCS-mcm
  type: service
  hostname: jbcs-eap
  path: /mcm/
  port: 443
- title: SSO-console
  type: service
  hostname: jbcs-eap
  path: /auth/
  port: 443
difficulty: basic
timelimit: 600
---
 💡 Single Sign-On deployment
===
#### Estimated time to complete: *20 minutes*<p>


☑️ Task 1 - Load the repository directory in the editor
===

1. Go to the **editor** tab, clicking on the link in topbar; if the git repository is still open from the previous challenge, proceed to Task 2 below.
2. In the **editor** tab, click on the File menu, then **Load directory**
3. Select the **eap-sso** directory, which is the working copy of the git repository
4. Click **OK** and then confirm in the dialog that open, that you trust the contents


☑️ Task 2 - Add a Single Sign-On playbook
===

☑️ Task 3 - Config Single Sign-On group variables
===

☑️ Task 4 - Locate and run the deploy Template
===

1. Switch to the **Automation controller** tab
2. On the side navigation bar, under the **Resources** section, click on **Templates**
3. Click on the **sso-eap-deploy** template
4. On the page that opens, click the **Launch** button
5. The launch dialog opens the **Survey**, asking for credentials (defaults are already set), click **Next**
6. Click **Launch**; you will be redirected the executing job output page.

☑️ Task 5 - Validate deployment
===


✅ Next Challenge
===
Press the `Check` button below to go to the next challenge once you’ve completed the task.

🐛 Encountered an issue?
====

If you have encountered an issue or have noticed something not quite right, please [open an issue](https://github.com/ansible-middleware/instruqt/issues/new?labels=a4mw-eap-sso&title=Issue+with+Deploy+Red+Hat+Single+Sign-On+with+Ansible+for+Middleware+collections+slug+ID:+a4mw-eap-sso-collections&assignees=guidograzioli).

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
