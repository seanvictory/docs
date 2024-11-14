---
description: >-
  Connect your Git repository to sync changes made in Paragon to a version
  control system.
---

# Setting up Git Sync

You can sync your Paragon project with GitHub using Git Sync, allowing you to easily incorporate Paragon into your version control and code review processes.

When Git Sync is enabled, any changes made to your integrations or workflows in the Paragon dashboard will automatically sync to your connected Git repository as [Paragraph](getting-started.md) files.

<figure><img src="../.gitbook/assets/image (85).png" alt=""><figcaption></figcaption></figure>

## How syncing works

Git Sync works by automating CLI commands with GitHub Actions, in response to change events in Paragon or in your Git repository. You can opt into a bidirectional sync or a one-way sync, depending on what works best for your team:

* **Bidrectional sync**: Both engineering and non-engineering team members will be working on integrations development, editing in both code and the workflow editor.
* **One-way sync from Git -> Paragon**: Paragraph code will be the source of truth, and updates to integrations will strictly be made in code. Works best when only engineering team members will be working on integrations development, or where advanced patterns like higher-order steps or modular workflow fragments are required.
* **One way sync from Paragon -> Git**: Paragon dashboard will be the source of truth, and updates will sync back to Git as a more fine-grained form of version control.

{% hint style="warning" %}
**Limitations**

* If you are using advanced patterns in Paragraph, such as reusable steps, higher-order steps, or modular workflow fragments, Git Sync currently cannot recover the use of these abstractions in code.
* When making updates in a dashboard to a workflow that is using advanced patterns in Paragraph, the advanced pattern will be a replaced with an inline representation of the resulting steps.
* If these limitations affect you, you can opt in to a one-way Git Sync from Git -> Paragon.
{% endhint %}

## Setup

### Repository setup

First, we'll need to set up a GitHub repository to sync your integrations with.

1. If you don't already have one, create a new GitHub repository. This repository can be public or private.
2. Push the contents of your initialized Paragraph project to your repository: [#exporting-from-paragon](getting-started.md#exporting-from-paragon "mention").
3. Add and commit new files called `.github/workflows/paragraph-push.yml` and `.github/workflows/paragraph_pull_runner.yml` at the root of your repository with the contents of the **GitHub Actions workflow files** below.
4. Navigate to your GitHub repository and select Settings. Navigate to **Secrets and variables > Actions**.
5. Create a repository secret for `PARAGON_CLI_KEY`. You can find this value on your machine in the file `~/.paragon/credentials.json`. It will be the value within `token` in this file.

<details>

<summary>GitHub Actions workflow files</summary>

### **Git -> Paragon** (`paragraph-push.yml`)

Any commits that you write to your Git repository will trigger a CI workflow that builds and pushes the contents back to the Paragon dashboard.

```yaml
name: Push to Paragon

on:
    push:
        # Set this to your selected branch in Paragon
        branches: [ "main" ]

    # Allows you to run this workflow manually from the Actions tab
    workflow_dispatch: 

jobs:
  push_to_paragon:
    name: Push to Paragon
    runs-on: ubuntu-latest
      
    steps:
      - uses: actions/checkout@v4
      - id: push
        uses: useparagon/paragraph-push@v1
        with:
          paragonKey: ${{ secrets.PARAGON_CLI_KEY }}
          paragonZeusUrl: https://zeus.useparagon.com
          paragonDashboardUrl: https://dashboard.useparagon.com
```

### **Paragon -> Git** (`paragraph_pull_runner.yml`)

Any changes that you make from the dashboard will trigger a CI workflow. This workflow will re-export the contents of your Paragon project into Paragraph, committing the resulting diff.

```yaml
name: Pull from Paragon

on: 
  workflow_dispatch:
    inputs:
      projectId:
        type: string
        required: true
        description: 'Paragon project id'

      commitId:
        type: string
        required: true
        description: 'Paragon project commit id'

jobs:
  pull_from_paragon:
    name: Pull from Paragon
    runs-on: ubuntu-latest

    permissions:
      contents: write
      
    steps:
      - uses: actions/checkout@v4
      - id: pull
        uses: useparagon/paragraph-pull@v1
        with:
          projectId: ${{ inputs.projectId }}
          commitId: ${{ inputs.commitId }}
          paragonKey: ${{ secrets.PARAGON_CLI_KEY }}
          paragonZeusUrl: https://zeus.useparagon.com
          paragonDashboardUrl: https://dashboard.useparagon.com
```

</details>

### Token setup

Next, you'll need to generate a GitHub Personal Access Token (PAT) to use in the Paragon dashboard.

1. In GitHub [Developer Settings](https://github.com/settings/tokens), click the Fine-grained tokens section in the Personal access tokens sidebar.
2. Generate a new token. Specify a descriptive name like "Paragon Git Sync" and desired expiration.
3. Select the repository owner/organization as the Resource Owner of the token.\
   If your organization is not appearing in the list of available Resource Owners, you may need to ask your GitHub organization admin to allow PATs in your organization (see [GitHub docs](https://docs.github.com/en/organizations/managing-programmatic-access-to-your-organization/setting-a-personal-access-token-policy-for-your-organization#restricting-access-by-fine-grained-personal-access-tokens)).
4. Select your intended integrations repository in Repository Access.
5.  Select the following Permissions:\
    \
    **Actions:** Read and write\
    **Contents**: Read only\
    **Metadata:** Read only\
    **Members**: Read only\
    \
    The Overview of the Permissions should look like:\


    <figure><img src="../.gitbook/assets/image (86).png" alt="" width="375"><figcaption></figcaption></figure>
6. Generate the token.
7. In the Paragon dashboard, click "Sync git branch" in the top navigation bar.
8. Paste your PAT and press Connect.
9. Select a repository to sync Paragon with.
10. Select which branch of your Git repository your Paragon project should sync with. Each Paragon project can be associated with a different branch in your Git repository.

{% hint style="warning" %}
**Note**: If your fine-grained PAT requires admin approval, you will immediately receive a generated token value, but the permissions will not be granted until the admin approves the token. Please verify that your token has been approved before proceeding.
{% endhint %}

Git Sync works with both classic and fine-grained PATs, but we recommend using a fine-grained PAT to generate a token with least-access privileges. See below for classic token instructions.

<details>

<summary>Setup instructions for classic Personal Access Tokens</summary>

Generate a classic Personal Access Token with the following scopes:

* `repo`
* `workflow`
* `read:org`
* `admin:repo_hook`
* `read:user`

Paste this value into the Paragon dashboard, under "Sync git branch".

</details>

## Syncing changes

As you make changes to your integrations in the Paragon dashboard, your changes will be synced as commits to your connected Git repository.

Workflow changes can be synced immediately by clicking ![](<../.gitbook/assets/Workflow Editor three dot menu (1).png>) **> Save Version** in the Workflow Editor.

You can view the sync history for your Paragon project by clicking the Sync Status icon in the navigation bar of the Paragon dashboard.

<figure><img src="../.gitbook/assets/App Event Page.png" alt=""><figcaption></figcaption></figure>

If you are not seeing changes appear in the dashboard or in your Git repository, verify your token permissions in [#token-setup](setting-up-git-sync.md#token-setup "mention").
