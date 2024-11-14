---
description: Configure your managed Paragon instance on GCP.
---

# Configuring Managed GCP

## Overview

[Paragon](https://www.useparagon.com/) allows customers the option of self-hosting Paragon on your own infrastructure. All the resources live in your AWS, Azure or GCP account GCP, and data never leaves your cloud.

We provide a managed on-prem solution at no additional cost. In this model, our enterprise team will take care of deploying, configuring, and managing your installation to offload almost 100% of developer time while providing the security and transparency of owning the resources and confidence that other resources in your Azure account are inaccessible.

### Security

We use the principle of least privileged access to grant the Paragon installer the access it needs to create and manage resources in your account. For GCP customers, we recommend a combination of GCP projects and service accounts for RBAC (role based access control). With this method:

* a new project is created on your GCP account with resources created belonging to that porject
* a new service account is created on your GCP account to manage resources in the project to be used by the Paragon installer

## Setup

The only thing that we need provide is the JSON config for the service account used by the installer.

### Directions

1. Login to your GCP console as an admin.
2. Create a project.
   1. In the top left corner (near the **Google Cloud Platform** logo), click the dropdown for your currently active project.
   2. In the modal that appears, click **New Project.**
   3. Name the project **Paragon**.
3. Make sure the newly created project is the currently active one.
4. Create a service account.
   1. Click **IAM & Admin** in the left sidebar.
   2. Click **Service Accounts**.
   3. Click **Create Service Account**.
   4. Make the service account an **Owner** of the project.
   5. Name the account **Paragon Installer**.
5. Retrieve the auth configuration.
   1. Click the newly created service account.
   2. Navigate to **Keys**.
   3. Click **Add Key**.
   4. Generate a JSON file.
   5. Download the file.

## Next Steps

Once all of this is done, provide us the newly created service account file, and we’ll setup your installation!

If you have any questions, email [**enterprise@useparagon.com**](mailto:enterprise@useparagon.com) for help.
