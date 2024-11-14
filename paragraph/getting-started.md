---
description: >-
  Paragraph allows you to author and maintain Paragon integrations as code,
  which can be synced with a Git repository to track revisions over time.
cover: ../.gitbook/assets/Frame 1000002911 (2).png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Getting Started with Paragraph

With Paragraph, your engineering team can:

* Define all your integrations powered by Paragon as code, while still being able to view, edit, and debug from the dashboard
* Version control all changes to your integrations in a Git repository, which can be used to bring code review, unit testing, and CI/CD to your development process
* Use more advanced abstractions in Workflows, including reusable steps or modularizing workflow logic across integrations

{% embed url="https://www.youtube.com/watch?v=eD2a7LlCjQM" %}

### Overview

Paragraph is a TypeScript-based framework for building your Paragon integrations in code. In a Paragraph project, you'll define:

* Integrations that are available to your users
* [Connect Portal configuration](../connect-portal/connect-portal-customization.md), including [User Settings](../connect-portal/workflow-user-settings.md) and [Field Mappings](../connect-portal/field-mapping.md)
* [Workflows](broken-reference), including [Triggers](../workflows/triggers/) and Steps

Paragraph projects can be packaged and sent to Paragon for deployment using the Paragon CLI or [from your CI/CD](setting-up-git-sync.md).

You can also continue to use the Paragon dashboard to edit your projects. By [setting up Git Sync](setting-up-git-sync.md), you can sync back changes made in the Paragon dashboard to your Paragraph project, stored in a Git repository.

<details>

<summary>What isn't defined in a Paragraph project?</summary>

Paragraph represents your integration business logic and doesn't include some types of configuration values that are specified in the dashboard.

The following configuration values must be maintained using the dashboard and will have no representation in your Paragraph project:

* [Environment Secrets](../workflows/environment-secrets.md): Sensitive values that are used in Workflows are defined and managed in the dashboard, in Project Settings.
* [Signing Keys](../getting-started/installing-the-connect-sdk.md#setup-with-your-own-authentication-backend): The private key used to sign Paragon User Tokens is generated and managed in the dashboard, in Project Settings.
* [Client ID and Secret](../getting-started/adding-an-integration.md#connect-your-developer-app-to-paragon): Any sensitive credentials representing your OAuth app with an integration are managed in the Settings tab of any integration.
* Scopes: Scopes requested by your OAuth app are also managed in the Settings tab of any integration.
  * For Custom Integrations, scopes are included in the Paragraph config file.
* [Team Members](broken-reference): Users and roles that have access to your Paragon organization are managed in the dashboard, in Organization Settings.

</details>

{% hint style="success" %}
For a personalized onboarding to Paragraph, you can [book time](https://calendly.com/ethan-paragon/paragraph-beta-onboarding) with our team to get started.
{% endhint %}

### Installing the CLI

#### Installing the CLI and authorizing your account

To begin setting up Paragraph project, you'll need to install the Paragon CLI. You can install the CLI globally with npm:

```
npm install -g @useparagon/cli
```

Once installed, the CLI will be available as the alias `para`. See [Broken link](broken-reference "mention") for the full reference for available CLI commands.

You can link your Paragon account to the CLI by running:

```
para auth login
```

<details>

<summary>Using an on-prem environment?</summary>

You can authenticate to the CLI from your on-premises environment with the `--host` flag:

```
para auth login --host https://dashboard.yourhost.paragon.so
```

</details>

Follow the CLI prompt to login to Paragon and authorize the CLI. When you successfully log in, you should see:

```
Logged in as [Your Name] (yourname@email.com)
```

Authenticating with the CLI generates a CLI Key which is stored locally in `~/.paragon/credentials.json`. You can view and revoke CLI Keys in the dashboard in **Settings > CLI Keys**.

### Starting a Paragraph Project

#### Exporting from Paragon

You can export a Paragraph project from your Paragon dashboard by using the CLI:

```
para init --create-from-existing
```

A project selector will appear to choose a project to export as a Paragraph project.

#### Initializing an empty project

Alternatively, you can initialize a new Paragon project with the CLI:

```
para init new-project-name
```

#### Cloning an existing project

If you are cloning an existing Paragraph repository that a teammate started, make sure to install dependencies in the project:

```
git clone git@github.com:useparagon/integrations.git
para install
```

### Creating a new integration

Create a new integration in Paragraph with the CLI:

```
para new integration
```

A prompt will appear to select the integration you'd like to add. Once selected, a new folder for the integration will appear in your `src/` folder.&#x20;

_Learn more about how to configure an integration in_ [_Defining Integrations_](defining-integrations.md)_._

### Creating a new workflow

Start building a new workflow in an existing integration with the CLI:

```
para new workflow --integration salesforce
```

Specify the name of the integration folder, e.g. `salesforce` in the `--integration` flag. A prompt will appear to title the workflow. A new TypeScript file will appear in the `src/integrations/[integration]` subfolder.

_Learn more about workflows and how to define and orchestrate steps in_ [_Defining Workflows_](defining-workflows.md)_._

### Building and pushing

Once you are ready to push your changes back to the Paragon dashboard, you can use the CLI to validate your project and push to Paragon:

```
para build
```

_Learn more about handling build errors in_ [_Build and Push_](build-and-push.md)_._

Once you see a message confirming that a build has been created, use the CLI to upload to the Paragon platform:

```
para push
```

{% hint style="info" %}
Try [**Git Sync**](setting-up-git-sync.md) to configure an integration between your Paragraph files stored in a Git repository and your Paragon project.

Git Sync keeps your Paragon project and Paragraph repository automatically in-sync.
{% endhint %}
