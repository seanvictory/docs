---
description: Configure your managed Paragon instance on Azure.
---

# Configuring Managed Azure

## Overview

[Paragon](https://www.useparagon.com/) allows customers the option of self-hosting Paragon on your own infrastructure. All the resources live in your AWS, Azure, or GCP, and data never leaves your cloud.

We additionally offer a Managed On-Premise solution that almost 100% of our on-prem customers use at no additional cost. In this model, our enterprise team will take care of deploying, configuring, and managing your installation to offload 100% of developer time while providing the security and transparency of owning the resources and confidence that other resources in your Azure account are inaccessible.

### Security

We use the principle of least privileged access to grant the Paragon installer the access it needs to create and manage resources in your account. For Azure customers, we recommend a combination of Azure Tenants, Azure Subscriptions, and RBAC (role-based access control). With this method:

* a new tenant is created on your Azure account with resources created belonging to that tenant and separate from all other resources
* a new subscription is created to associate all Paragon resources created within that tenant
* a role is created to manage resources in the subscription for that tenant and provided to the installer

Using this method, extra redundancies are put in place that ensures Paragon can only interact with the intended resources while providing a means for you to transparently view all resources created, separate billing to manage the resources while being connected to a parent account, and have super user access for all resources created.

## Setup

We’ll need 4 values to install Paragon.

* Tenant Id
* Subscription Id
* Client Id
* Client Secret

### Directions

1. Login to your Azure portal as an admin.
2. Create a tenant.
   1. Search _<mark style="color:red;">**`Azure Active Directory`**</mark>_ in the search bar, navigate to your **Azure Active Directory**, and click the **Manage tenants** tab.
   2. Click **+ Create.**
   3. Select **Azure Active Directory** as the tenant type in the **Basics** tab.
   4. Click the **Configuration** tab.
   5. Enter _<mark style="color:red;">**`Paragon`**</mark>_ as the Organization name.
   6. Enter a domain name with _<mark style="color:red;">**`paragon`**</mark>_ and your organization’s name, i.e. _<mark style="color:red;">**`paragongoogle`**</mark>_. The domain must be alphanumeric.
   7. Click the **Review + create** tab.
   8. Click the **Create** button to create the tenant.
   9. Search _<mark style="color:red;">**`Azure Active Directory`**</mark>_ in the search bar, navigate to your **Azure Active Directory**.
   10. ⭐️ Copy the text in the _Overview_ section next to _Tenant ID_. This is the **Tenant Id.** ⭐️
3. Create a subscription under the tenant.
   1. Switch to your default Azure directory. You can do this by clicking your account in the top right corner and clicking **Switch directory.**
   2. Search _<mark style="color:red;">**`Subscriptions`**</mark>_ in the search bar, and navigate to your **Subscriptions**.
   3. Click **+Add**
   4. In the **Basics** tab, enter _<mark style="color:red;">**`Paragon`**</mark>_ for the Subscription name.
   5. Click the **Advanced** tab and select the new tenant you created for the Subscription directory.
   6. Click the **Review + create** tab.
   7. Confirm the name of the subscription is correct in the _Basics_ section and the correct tenant is selected in the _Advanced_ section.
   8. Click **Create**.
   9. ⭐️ Copy the id of the subscription. This is the **Subscription Id.** ⭐️
4. Create credentials for the Paragon installer.
   1. Switch to the new Paragon directory. You can do this by clicking your account in the top right corner and clicking **Switch directory.**
   2. Search _<mark style="color:red;">**`Azure Active Directory`**</mark>_ in the search bar, navigate to your **Azure Active Directory**, and click the **App registrations** tab.
   3. Click **+ New registration.**
   4. Enter _<mark style="color:red;">**`Paragon Installer`**</mark>_ for the name of the application.
   5. Select _<mark style="color:red;">**`Accounts in this organizational directory only`**</mark>_ for the access type.
   6. Leave the _Redirect URI (optional)_ field empty.
   7. Click **Create** to create the application.
   8. ⭐️ Save the text next to _Application (client) ID_. This is the **Client Id**. ⭐️
   9. Click **Add a certificate or secret** next to _Client credentials_.
   10. Click **+ New client secret** to create a new secret.
   11. Enter _<mark style="color:red;">**`Paragon Installer`**</mark>_ for the description.
   12. Select _<mark style="color:red;">**`24 months`**</mark>_ for _Expires._
   13. Click **Add** to create the secret.
   14. ⭐️ Save the text under the _Value_ column. This is the **Client Secret**. ⭐️
5. Give the new _Paragon Installer_ application access to manage the newly created subscription.
   1. Search _<mark style="color:red;">**`Subscriptions`**</mark>_ in the search bar, and navigate to your **Subscriptions**.
   2. Click the newly created _Paragon_ subscription.
   3. Click **Access control (IAM)** in the left sidebar.
   4. Click **+ Add** and select **Add role assignment**.
   5. Search _<mark style="color:red;">**`Contributor`**</mark>_ and click **View** on the right side.
   6. Click **Select role** at the bottom of the sidebar that opened.
   7. Click the **Members** tab and click **+ Select members**.
   8. Search _<mark style="color:red;">**`Paragon Installer`**</mark>_ and select the application.
   9. Click the **Select** button at the bottom of the sidebar.
   10. Click **Review + assign** to assign the role.

## Next Steps

Once all of this is done, provide us with these four values, and we’ll set up your installation!

If you have any questions, email [**enterprise@useparagon.com**](mailto:enterprise@useparagon.com) for help.
