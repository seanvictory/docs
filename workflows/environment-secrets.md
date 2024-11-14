---
description: Securely store and access credentials across your workflows.
---

# Environment Secrets

## Overview

Environment Secrets are global variables used for securely storing and accessing secure values across your workflows. For example, you can store a global authorization token for your API to use in all Request steps that send a request to your API.

{% hint style="info" %}
**Note:** You must be an account Admin to manage Environment Secrets.
{% endhint %}

To set up Environment Secrets:

**1. Click on "Settings" in the sidebar, then click on "Environment Secrets".**&#x20;

![](<../.gitbook/assets/Going to settings in Paragon.gif>)

**2. Enter details for your new Environment Secret.**

Set **Key** to a descriptive and recognizable name. This easily identifies it in the variable menu.

![](<../.gitbook/assets/Creating environment secrets in Paragon.gif>)

## Using Environment Secrets

Environment Secrets appear at the bottom of the variable menu. Selecting one uses the `Value` stored in the Environment Secret.

![](<../.gitbook/assets/Using environment secrets in Paragon.gif>)

## Updating an Environment Secret

Click on the triple-dot menu to the right of the Environment Secret you'd like to update. After confirming the update, the Environment Secret will update in any workflows it's used in.

![](<../.gitbook/assets/Updating environment secrets in Paragon.gif>)

## Deleting an Environment Secret

Click on the triple-dot menu to the right of the environment secret you'd like to delete. After confirming the deletion, the Environment Secret will get removed from any workflows.

![](<../.gitbook/assets/Deleting environment secrets in Paragon.gif>)
