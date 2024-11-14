---
description: Configure your managed Paragon instance on AWS.
---

# Configuring Managed AWS

## Overview

To run Paragon's software on your AWS account, you'll need to use [AWS Organizations](https://aws.amazon.com/organizations/). AWS Organizations allows you to create new AWS accounts with sandboxed resources, policies and billing completely separate from your own.

We additionally offer a Managed On-Premise solution that is used by most of our on-premise customers. In this model, our enterprise team is responsible for deploying, configuring, and managing your installation to offload 100% of developer time while providing the security and transparency of owning the resources and confidence that other resources in your AWS account are inaccessible.

### Security

We use the principle of least privileged access to grant the Paragon installer the access it needs to create and manage resources in your account. When creating an AWS Account, all resources are completely sandboxed within that account and the installer can’t access anything outside of it. Any VPCs, databases, servers, etc on your primary AWS account can’t be accessed from this account.

## Setup

## AWS Organization

**Time required**: 5 minutes

1. Visit the [AWS Organizations](https://console.aws.amazon.com/organizations/home?#/accounts) dashboard and login with an admin account.
2. Click **Add account**.
3. Click **Create account**.
4. Fill in the details
   1. **Account name:** Paragon
   2. **Email address:** [enterprise+YOUR\_ORGANIZATION@useparagon.com](mailto:enterprise+YOUR\_ORGANIZATION@useparagon.com) e.g. [_enterprise+google@useparagon.com_](mailto:enterprise+google@useparagon.com)
5. That's it. We'll set it up from there 🚀
