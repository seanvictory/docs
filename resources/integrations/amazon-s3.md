---
description: Connect to your users' Amazon S3 accounts.
---

# Amazon S3

## Setup Guide

You can find your Amazon S3 app credentials in your [Amazon S3 Developer Account.](https://docs.aws.amazon.com/AmazonS3/latest/API/Type\_API\_Reference.html)

You'll need the following information to set up your Amazon S3 App with Paragon Connect:

* API Key

## Connecting to Amazon S3

Once your users have connected their Amazon S3 account, you can use the Paragon SDK to access the Amazon S3 API on behalf of connected users.

See the Amazon S3 [REST API documentation](https://docs.aws.amazon.com/AmazonS3/latest/API/Type\_API\_Reference.html) for their full API reference.

Any Amazon S3 API endpoints can be accessed with the Paragon SDK as shown in this example.

```javascript
// You can find your project ID in the Overview tab of any Integration

// Authenticate the user
paragon.authenticate(<ProjectId>, <UserToken>);
            
// Get an Object
await paragon.request("amazons3", "/<Bucket>/<Key>", {
  method: "GET"
});

// Create a Bucket
await paragon.request("amazons3", "/<Bucket>", {
  method: "PUT",
  body: `<?xml version="1.0" encoding="UTF-8"?>
<CreateBucketConfiguration xmlns="http://s3.amazonaws.com/doc/2006-03-01/">
   <LocationConstraint>us-east-2</LocationConstraint>
</CreateBucketConfiguration>`
});
  
```

## Building Amazon S3 workflows

Once your Amazon S3 account is connected, you can add steps to perform the following actions:

* Create Folder
* Delete Folder
* Upload File
* Download File
* List Files

You can also use the Amazon S3 Request step to access any of Amazon S3's API endpoints without the authentication piece.

When creating or updating records in Amazon S3, you can reference data from previous steps by typing `{{` to invoke the variable menu.
