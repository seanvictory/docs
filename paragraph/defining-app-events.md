---
description: Learn how to define App Event schemas in Paragraph projects.
---

# Defining App Events

[App Events](../workflows/triggers/#app-events) are JSON payloads that can be used to trigger workflows from your application, using the SDK or API. In Paragraph, you can define an App Event with a file that declares its name and schema.

### Creating a new App Event

App Events reside in the `src/events` folder of your Paragraph project. You can create a new file, like `src/events/newTask.ts`, to define a new type of App Event.

```typescript
import { IEventInit } from '@useparagon/core/event';

export type EventSchema = {
  title: 'Example Title';
  description: 'Example Description';
  storyPointEstimate: 0;
};

const event: IEventInit<EventSchema> = {
  /**
   *  name of event
   */
  name: 'New Task',

  /**
   * schema of event payload
   */
  schema: {
    title: 'Example Title',
    description: 'Example Description',
    storyPointEstimate: 0,
  },
};

export default event;
```

The file must export a default object that includes the name of the event (which will be used in the SDK and the API when App Events are sent) and an example payload.

### Using an App Event in a Workflow

To use the App Event in a workflow file, import the event into the Workflow:

```typescript
import newTaskEvent from "../../../events/newTask";
```

{% hint style="danger" %}
Currently, relative imports are required to be used from Workflow files. Avoid using absolute imports, e.g. `src/events/newTask`.
{% endhint %}

Then, you can pass the event into an `EventStep` trigger as the first step in the Workflow:

```typescript
const triggerStep = new EventStep(newTaskEvent);
```
