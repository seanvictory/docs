---
description: >-
  In this tutorial, we'll use the Paragon SDK to build an integrations catalog
  into your app.
---

# Building an In-App Integrations Catalog

This guide provides an example implementation of building an integrations catalog **into your React app, using TypeScript.** The completed code is available in [this GitHub repository](https://github.com/useparagon/paragon-integrations-catalog-tutorial).

{% hint style="info" %}
The tutorial repository signs Paragon User Tokens in the frontend application, which should NOT be used in production. Replace `getParagonUserToken` with your own app's Paragon User Token generation, which should be performed on your server only.
{% endhint %}

Alternatively, for a production-ready implementation of the SDK embedded in a Next.js app, see our [Example App](https://github.com/useparagon/paragon-connect-nextjs-example) repository.

### Demo

In this tutorial, we'll build the user interface to display a list of Paragon integrations embedded in your application:

<figure><img src="../.gitbook/assets/Screen Recording.gif" alt=""><figcaption></figcaption></figure>



### Prerequisites

* This guide embeds the Integration Catalog in a React.js app. React is not a requirement for using the SDK, but the tutorial steps will use React-specific functions to dynamically update the Catalog UI.
* This guide assumes that you've already [installed the SDK and configured User Authentication](../getting-started/installing-the-connect-sdk.md). We will change your implementation slightly so that your React app can listen for the SDK events for loading and authenticating.

## 1. Add hooks for authenticating the Paragon User

First, define a hook used for SDK authentication. We'll call this `useParagonAuth.ts`. Copy the following contents to this file:

```typescript
import { useEffect, useState } from "react";
import { paragon, AuthenticatedConnectUser } from "@useparagon/connect";

async function getParagonUserToken(): Promise<string> {
  // Replace this with the logic that your app uses for
  // fetching the Paragon User Token.
}

export default function useParagonAuth(): { user?: AuthenticatedConnectUser; error?: Error } {
  const [token, setToken] = useState<string | null>(null);
  const [user, setUser] = useState<ConnectUser | undefined>();
  const [error, setError] = useState<Error | undefined>();

  useEffect(() => {
    getParagonUserToken().then(setToken).catch(setError);
  }, []);

  useEffect(() => {
    if (token && !error) {
      paragon
        .authenticate(PARAGON_PROJECT_ID, token)
        .then(() => setUser(paragon.getUser()))
        .catch(setError);
    }
  }, [token, error]);

  return { user, error };
}
```

{% hint style="info" %}
Replace `PARAGON_PROJECT_ID` with your Project ID in Paragon. You can find your Project ID in the Overview tab of any Integration within the dashboard.
{% endhint %}

This hook can then be consumed from a component that will render your integrations catalog as follows:

```typescript
// IntegrationsCatalog.tsx
import useParagonAuth from "../hooks/useParagonAuth";

function IntegrationsCatalog() {
    const { user } = useParagonAuth();
    
    return (<div className="catalog">
        <h1>Integrations Catalog</h1>
    </div>);
}

export default IntegrationsCatalog;
```

## 2. Displaying integrations

Next, we'll show the list of integrations loaded from your project. The `paragon` global is loaded as a stateful value, so when the SDK loads, the component will update accordingly:

<pre class="language-typescript"><code class="lang-typescript">// IntegrationsCatalog.tsx
<strong>import { paragon } from "@useparagon/connect";
</strong>
function IntegrationsCatalog() {
    const { user } = useParagonAuth();
    
    return (&#x3C;div className="catalog">
        &#x3C;h1>Integrations Catalog&#x3C;/h1>
<strong>        {paragon.getIntegrationMetadata().map((integration) => {
</strong><strong>             return &#x3C;div
</strong><strong>                 key={integration.type}
</strong><strong>                 onClick={() => paragon.connect(integration.type)}
</strong><strong>             >
</strong><strong>                 &#x3C;img src={integration.icon} width={20} height={20} />
</strong><strong>                 &#x3C;p>{integration.name}&#x3C;/p>
</strong><strong>             &#x3C;/div>;
</strong><strong>         })}
</strong>    &#x3C;/div>);
}

export default IntegrationsCatalog;
</code></pre>

This snippet calls [`.getIntegrationMetadata`](https://docs.useparagon.com/api/api-reference#.getintegrationmetadata) to get all active integrations in your project, along with their names and icon URLs.

For every integration, we display their icons and names. We also set up an event handler to call [`.connect`](https://docs.useparagon.com/api/api-reference#.connect-integrationtype-string) with the `integration.type` when the element is clicked. This will display the Connect Portal over your app, prompting the user to connect an account to the specified integration.

**Result:**

<figure><img src="../.gitbook/assets/Recording 2022-11-07 at 09.08.22.gif" alt=""><figcaption><p>When you click on any one of the integrations, the Connect Portal overlay appears over your app.</p></figcaption></figure>

## 3. Displaying account status

Next, we'll update your integrations catalog to display your user's account status for each integration within the element that shows the icon and name.

We can get the account status using [`.getUser`](https://docs.useparagon.com/api/api-reference#.getuser-paragonuser), which returns the current state of the authenticated user from the SDK, including their connected integrations and enabled workflows.

<pre class="language-typescript"><code class="lang-typescript">// IntegrationsCatalog.tsx
import { paragon } from "@useparagon/connect";

function IntegrationsCatalog() {
    const { user } = useParagonAuth();
    
    return (&#x3C;div className="catalog">
        &#x3C;h1>Integrations Catalog&#x3C;/h1>
        {paragon &#x26;&#x26;
         paragon.getIntegrationMetadata().map((integration) => {
<strong>             const integrationEnabled = user?.integrations?.[integration.type]?.enabled;
</strong>             return &#x3C;div
                 key={integration.type}
                 onClick={() => paragon.connect(integration.type)}
             >
                 &#x3C;img src={integration.icon} width={20} height={20} />
                 &#x3C;p>{integration.name}&#x3C;/p>
<strong>                 &#x3C;p>{integrationEnabled ? "Connected" : "Not connected"}&#x3C;/p>
</strong>             &#x3C;/div>
         })}
    &#x3C;/div>);
}

export default IntegrationsCatalog;
</code></pre>

**Result:**

<figure><img src="../.gitbook/assets/image (20).png" alt=""><figcaption><p>Each integration will show the "Connected" or "Not connected" status for the current user.</p></figcaption></figure>

## 4. Adding subscriptions for account status changes

Finally, we want to make sure that the catalog components that we've created update automatically when the SDK handles a state change with one of our user's integrations. Specifically, when a user connects or disconnects their account, we want the account status to reflect that immediately.

To do this, we can use [`.subscribe`](https://docs.useparagon.com/api/api-reference#subscribe), which allows us to listen for global SDK events. We will listen for the events `"onIntegrationInstall"` and `"onIntegrationUninstall"` to detect when a user has connected or disconnected an account.

<pre class="language-typescript"><code class="lang-typescript">// useParagonAuth.ts
<strong>import { paragon, AuthenticatedConnectUser, SDK_EVENT } from '@useparagon/connect';
</strong>
export default function useParagonAuth(): { user?: AuthenticatedConnectUser; error?: Error } {
  const [token, setToken] = useState&#x3C;string | null>(null);
  const [user, setUser] = useState&#x3C;ConnectUser | undefined>();
  const [error, setError] = useState&#x3C;Error | undefined>();

  useEffect(() => {
    getParagonUserToken().then(setToken).catch(setError);
  }, []);
  
<strong>  // Listen for account state changes
</strong><strong>  useEffect(() => {
</strong><strong>    const listener = () => {
</strong><strong>        const authedUser = paragon.getUser();
</strong><strong>        if (authedUser.authenticated) {
</strong><strong>          setUser({ ...authedUser });
</strong><strong>        }
</strong><strong>    };
</strong><strong>    paragon.subscribe(SDK_EVENT.ON_INTEGRATION_INSTALL, listener);
</strong><strong>    paragon.subscribe(SDK_EVENT.ON_INTEGRATION_UNINSTALL, listener);
</strong><strong>    return () => {
</strong><strong>      paragon.unsubscribe(SDK_EVENT.ON_INTEGRATION_INSTALL, listener);
</strong><strong>      paragon.unsubscribe(SDK_EVENT.ON_INTEGRATION_UNINSTALL, listener);
</strong><strong>    };
</strong><strong>  }, []);
</strong>
  useEffect(() => {
    if (token &#x26;&#x26; !error) {
      paragon
        .authenticate(PARAGON_PROJECT_ID, token)
        .then(() => setUser(paragon.getUser()))
        .catch(setError);
    }
  }, [token, error]);

  return { user, error };
}
</code></pre>

Our integrations catalog will now re-render with the most up-to-date information when account state changes.

**Result**: You've completed a basic Integrations Catalog with the Connect SDK!

<figure><img src="../.gitbook/assets/Screen Recording.gif" alt=""><figcaption></figcaption></figure>

## Recap

In this guide, you built an integrations catalog that you can embed in your app.

* You defined 2 hooks: [`useParagonGlobal`](https://github.com/useparagon/paragon-integrations-catalog-tutorial/blob/master/src/hooks/useParagonGlobal.ts) (for mounting the Paragon SDK) and [`useParagonAuth`](https://github.com/useparagon/paragon-integrations-catalog-tutorial/blob/master/src/hooks/useParagonAuth.ts) (for authenticating a user).
* You used [`.getIntegrationMetadata`](https://docs.useparagon.com/api/api-reference#.getintegrationmetadata) to get all available integrations in the project with name and icon information.
* You used [`.getUser`](https://docs.useparagon.com/api/api-reference#.getuser-paragonuser) to get the user's account status.
* You used [`.subscribe`](https://docs.useparagon.com/api/api-reference#subscribe) to listen for user account status changes to sync updates to your catalog UI.

