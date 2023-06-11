---
slug: a4mw-eap-final-deploy
id: yjex4vndabmn
type: challenge
title: Final deployment
teaser: A last job template execution to put everything in order and accomplish our
  mission
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
- title: addressbook
  type: service
  hostname: jbcs-eap
  path: /addressbook/
  port: 443
difficulty: basic
timelimit: 600
---
---
 💡 Final Deployment
===
#### Estimated time to complete: *10 minutes*<p>

☑️ Task 1 - Locate and run the deploy Template
===

1. Switch to the **Automation controller** tab
2. On the side navigation bar, under the **Resources** section, click on **Templates**
3. Click on the **sso-eap-deploy** template
4. On the page that opens, click the **Launch** button
5. The launch dialog opens the **Survey**, asking for credentials (defaults are already set), click **Next**
6. Click **Launch**; you will be redirected the executing job output page.


✅ Workshop complete
===
Press the `Check` button below once you’ve completed the task. The workshop is completed!


🐛 Encountered an issue?
====

If you have encountered an issue or have noticed something not quite right, please [open an issue](https://github.com/ansible-middleware/instruqt/issues/new?labels=a4mw-eap-sso&title=Issue+with+Deploy+Red+Hat+Single+Sign-On+with+Ansible+for+Middleware+collections+slug+ID:+a4mw-eap-sso-final-deploy&assignees=guidograzioli).

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
