---
description: >-
  The Paragon SDK can be imported in your front-end JavaScript to embed the
  Connect Portal and trigger workflows in your application.
---

# Installing the SDK

## Installing from npm

You can install the Paragon SDK with npm:

```bash
npm install @useparagon/connect
```

The SDK can be imported in your client-side JavaScript files as a module:

```typescript
import { paragon } from '@useparagon/connect';
```

**For** [**on-premise**](broken-reference)**/single-tenant users:**

If you are using an on-prem/single-tenant instance of Paragon, you can call the `.configureGlobal` function to point the SDK to use the base hostname of your Paragon instance.

```typescript
import { paragon } from '@useparagon/connect';

// If your login URL is https://dashboard.mycompany.paragon.so:
paragon.configureGlobal({
    host: "mycompany.paragon.so"
});
```

<details>

<summary><strong>Migrating from the &#x3C;script> tag?</strong></summary>

If you are migrating from using the \<script> tag to the npm package, please note that `paragon` is no longer exposed as a global or on the `window` object by default.

Any references to `paragon` or `window.paragon` must be updated to point to the package import:

```diff
+ import { paragon } from '@useparagon/connect';

- window.paragon.authenticate(...);
+ paragon.authenticate(...);
```

</details>

## Setup

Before using the Paragon SDK, you'll need to set up your application to verify the identity of your users to the SDK.

Paragon verifies the identity of your users using the authentication system _you're already using,_ including managed services like Firebase or Auth0. Some backend code may be required if your application implements its own sign-in and registration.

If your application implements its own authentication backend, follow the steps in [Setup with your own authentication backend](installing-the-connect-sdk.md#setup-with-your-own-authentication-backend).&#x20;

If you use a managed authentication service like Firebase Authentication or Auth0, follow the steps in [Setup with a managed authentication service](installing-the-connect-sdk.md#setup-with-a-managed-authentication-service).

### Setup with your own authentication backend

If you use your own backend server to manage authentication, you'll first need to complete the following steps:

#### 1. Generate a Paragon Signing Key

To generate a Signing Key, go to **Settings > SDK Setup** in your Paragon dashboard. You should store this key in an environment secrets file.&#x20;

For security reasons, we don’t store your Private Key and cannot show it to you again, so we recommend you download the key and store it someplace secure.

<figure><img src="../.gitbook/assets/Generating a Signing Key in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

#### 2. Generate a Paragon User Token

Next, you'll need to generate a Paragon User Token for each of your authenticated users. To do this, you'll need a library in your target language to sign JWTs with RS256. You can find one in your language at [https://jwt.io/](https://jwt.io/).

If your application is a fully client-rendered single-page app, you may have to create and use an additional API endpoint to retrieve a signed JWT (or reuse an existing endpoint that handles authentication or user info).

The signed JWT/Paragon User Token minimally must include the `sub`, `iat`, and `exp` claims:

{% tabs %}
{% tab title="JavaScript" %}
```javascript
{
	// Uniquely identifying key for a user or their company
	"sub": "the-user/company-id",

	// Issue timestamp, should be the current time
	"iat": 1608600116

	// Expiry timestamp for token, such as 1 hour from time of signature (iat)
	"exp": 1608603716
}
```
{% endtab %}
{% endtabs %}

{% hint style="info" %}
#### Just for testing: Generating one-off JWTs

Use the [**Paragon JWT Generator**](https://paragon-jwt-generator-embedded.surge.sh/) to generate test JWTs for your development purposes. In production, static tokens should never be used.
{% endhint %}

#### **3. Call paragon.authenticate()**

You'll call `paragon.authenticate` in your view with a JWT signed by your backend using the library chosen in Step 2. **This JWT is the Paragon User Token.**

```javascript
await paragon.authenticate(
	// You can find your project ID in the Overview tab of any Integration
	"38b1f170-0c43-4eae-9a04-ab85325d99f7",

	// See Setup for how to encode your user token
	"eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.ey..."
);
```

The `paragon.authenticate` function is Promiseable and resolves when the SDK has successfully authenticated your user. Note that other functions, like `paragon.connect`, may not work as expected until this Promise has resolved.



**Example Implementation:** A Node.js and Express app using Handlebars view templating

1.  Adding middleware to sign the JWT and include it in the response context

    ```javascript
    // server.js - Adding middleware to sign an authenticated user's token
    const jwt = require('jsonwebtoken');

    app.use((req, res, next) => {
      if (!req.user) {
        return next();
      }
      // JWT NumericDates specified in seconds:
      const currentTime = Math.floor(Date.now() / 1000);
      res.locals({
        paragonToken: jwt.sign(
          {
            sub: req.user.id,  // Your user's or their company's ID
            iat: currentTime,
            exp: currentTime + (60 * 60), // 1 hour from now
          },
          process.env.PARAGON_SIGNING_KEY,
          {
            algorithm: "RS256",
          }
        ),
      });
      next();
    });
    ```
2.  Use the `paragonJwt` set in context within the view template, with a call to `paragon.authenticate`:

    ```markup
    // layout.hbs - Include paragon.authenticate call in the view template
    <body>
    	<script type="text/javascript">
    	  paragon.authenticate("project-id", "{{ paragonToken }}").then(() => {
    		  // paragon.getUser() will now return the authenticated user
    		});
    	</script>
    </body>
    ```

### Setup with a managed authentication service

You can set up managed authentication for your Paragon project by navigating to **Settings > SDK  Setup** and selecting a provider.

<figure><img src="../.gitbook/assets/Generating a Signing Key in Paragon Connect.png" alt=""><figcaption></figcaption></figure>

Since Paragon uses a JSON Web Token (JWT) to encode and validate user identity, many managed services will already have a token that you can pass directly to Paragon.

{% tabs %}
{% tab title="Firebase Authentication" %}
You'll need to provide Paragon with your **Firebase Project ID**, which you can find in the Firebase Console.

![](<../.gitbook/assets/Adding Firebase Authentication to Paragon Connect.png>)

The Firebase ID token can be used directly as the Paragon User Token.&#x20;

You can get a Firebase ID token from the [JavaScript client-](https://firebase.google.com/docs/auth/admin/verify-id-tokens#web)side library with:

```javascript
firebase.auth().currentUser.getIdToken(true).then(async function(idToken) {
	await paragon.authenticate("project-id", idToken);
})
```
{% endtab %}

{% tab title="Auth0" %}
You'll need to provide Paragon with your **Auth0 Tenant Domain**, which you can find ends with `.auth0.com`. Example: `https://<YOUR_TENANT>.auth0.com`.

If you have a domain alias for your tenant domain, use the domain alias instead.

![](<../.gitbook/assets/Adding Auth0 Authentication to Paragon Connect.png>)

The Auth0 ID token can be used directly as the Paragon User Token.

Auth0 provides [comprehensive docs](https://auth0.com/docs/tokens/id-tokens/get-id-tokens) on retrieving the ID token in various contexts. An example of this, using their [single page app SDK](https://auth0.com/docs/libraries/auth0-single-page-app-sdk#get-id-token-claims):

```javascript
auth0.getIdTokenClaims().then((claims) => {
	await paragon.authenticate("project-id", claims.__raw);
});
```
{% endtab %}
{% endtabs %}
