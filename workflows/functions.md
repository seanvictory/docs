# Using Functions

## Overview

Paragon's Functions are built-in cloud functions that provide a powerful way to add custom logic to your workflows. You can use functions to transform or compute data, or even to perform more complex operations within workflows that you might otherwise need to write server-side code for. Paragon functions support Javascript (ES7) and provide access to select npm modules.

{% content-ref url="../resources/javascript-libraries.md" %}
[javascript-libraries.md](../resources/javascript-libraries.md)
{% endcontent-ref %}

To add a function to your workflow, click the "+" button in the workflow canvas and choose the Function step from the sidebar.

![](<../.gitbook/assets/image (79).png>)

## Defining function parameters

You can pass any data from upstream steps into your Function as parameters using the key-value table under "What data should be passed in as parameters?". Under "Key", you can give your variable a name and under "Value" you can insert a variable from the variable menu by clicking the dropdown button.&#x20;

## Writing function code

You can write your custom code in the `yourFunction()` function, which accepts any valid Javascript (ES7). Any data that you `return` from this function can then accessed by downstream steps in your workflow.

You can access parameters defined in the key-value table above by referencing `parameters.<parameter_name>` within `yourFunction()`. For example, a parameter whose key is `email` can be accessed in the function by referencing `parameters.email`.

![](<../.gitbook/assets/Writing function code in Paragon.gif>)

## Using NPM modules in functions

Paragon provides access to [certain npm modules](../resources/javascript-libraries.md) that can be used within functions. Here's an example of how you can access the `uuid` npm module within a function.

{% tabs %}
{% tab title="JavaScript" %}
```javascript
function yourFunction(parameters, libraries) {
      // Generate a uuid with the uuid Javascript library
      const uuid = libraries.uuid;
      const id = uuid.v4();
      return id
}
```
{% endtab %}
{% endtabs %}

Note that you'll need to add the `libraries` parameter to `yourFunction()`. If your function needs to work asynchronously, you can declare it `async`.

![](<../.gitbook/assets/Using npm modules in functions in Paragon.gif>)

You can find the full list of supported npm modules in our [Javascript Libraries Catalog](../resources/javascript-libraries.md). If you don't see the module that you're looking for, [let us know](mailto:team@useparagon.com) and can usually add it for you.
