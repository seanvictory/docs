# Build and Push

## Building your project locally

After defining a workflow, you can use the `para` CLI to validate and build the workflow to prepare to upload it to the Paragon dashboard. Building workflows creates a subfolder in your project called `out/` with auto-generated files.

You can build all workflows in your project with the `build` command:

```bash
para build
```

If your build is successful, you will see:

```
✓ Typescript project successfully built.
✓ Created build in out/build.json file.
```

Otherwise, see [#diagnosing-build-errors](build-and-push.md#diagnosing-build-errors "mention") below to address build errors.

## Pushing your project to Paragon

{% hint style="info" %}
Try [**Git Sync**](setting-up-git-sync.md) to configure an integration between your Paragraph files stored in a Git repository and your Paragon project.

Git Sync keeps your Paragon project and Paragraph repository automatically in-sync.
{% endhint %}

To upload on a one-off basis to your Paragon project, use the `push` command in the CLI.

```bash
para push
```

* If your workflow has previously been pushed to your Paragon project, this command will _overwrite_ any changes that have been made to this workflow with the current contents of the Paragraph file that you are pushing.
* Workflows cannot be pushed to Staging or Production Release Environments. [Create a Release](../deploying-integrations/release-environments.md#creating-a-release) to move integration updates from Development -> Staging -> Production.

**Note: Paragraph projects are linked to the original project they were initialized from and cannot be changed.**

* Currently, you cannot use the `push` command to push or "copy" a project to a different Project ID. If your team requires this functionality, please reach out to discuss your needs and to get early access to a related feature we are working on: [support@useparagon.com](mailto:support@useparagon.com).
  * You can [create a Release](../deploying-integrations/release-environments.md#creating-a-release) to move integration updates from Development -> Staging -> Production.
* Do not attempt to modify `project.json` or `build.json` to do this, as you may inadvertently cause workflows to be moved across projects.

## Pulling changes from Paragon

To pull changes from the dashboard on a one-off basis to your Paragon project, **first commit all pending changes in your local repository**, and then use the `pull` command in the CLI.

```
para pull
```

* Any uncommitted changes may be overwritten by the `pull` command.
* As with the `push` command, any integrations or workflows that are absent from the source (your Paragon dashboard in the `pull` case) will be removed from the destination (the local repository). The best way to reconcile these types of removals is with [Git Sync](setting-up-git-sync.md), which will use your commits to sequence these changes.

## Diagnosing build errors

The build command operates in 2 phases:

1. A TypeScript compilation runs to check types for all of your workflows and integration configurations.
2. The compilation result is evaluated to produce a build artifact to upload to Paragon, in `out/build.json`.

If you are encountering TypeScript compilation errors, they will appear as follows:

```
src/integrations/hubspot/workflows/newWorkflow.ts:31:25 - error TS2554: Expected 1 arguments, but got 0.

31     const triggerStep = new EventStep();
                           ~~~~~~~~~~~~~~~
Found 1 error(s).
```

These errors are also visible in your editor, if you have a TypeScript language server running. TypeScript errors can be indicative of one of the following issues:

<table><thead><tr><th width="311">Problem</th><th>Resolution</th></tr></thead><tbody><tr><td><strong>Missing or invalid parameters</strong><br><br>Steps have incomplete configurations, which does not produce a valid workflow.</td><td>Visit the workflows with incomplete steps and correct their configuration.<br><br>If some workflow steps are intentionally incomplete (e.g. the workflow is a draft), you can prefix the filename with <code>~</code> to exclude it from the build.</td></tr><tr><td><strong>Incorrect step output path referenced</strong><br><br>A step requires output from other steps, but the path it references is not valid.</td><td>Visit the workflows with invalid step output paths and correct references to <code>.output</code>.<br><br>Use the TypeScript-powered autocomplete to help identify available properties.</td></tr><tr><td><strong>Function step code is using unknown properties</strong></td><td>Because Function step code in the dashboard does not use TypeScript, errors can appear in your exported Function steps about unsafely accessing properties in untyped values.<br><br>These errors can help refactor your Function step code to be type-safe, but you can ignore them by using <code>// @ts-ignore</code> above lines that are causing errors.</td></tr><tr><td><strong>Missing types from</strong> <code>@useparagon/integrations</code></td><td>Integration-specific dependencies may be missing from your project. Run <code>para install</code> with the CLI to pull in missing dependencies.</td></tr><tr><td><strong>Error</strong>: <code>persona.meta.js</code> is not found in project</td><td>This error may indicate that you have incorrectly imported modules in a workflow.<br><br>Check your import statements in workflows to verify that you are using relative paths instead of absolute paths:<br><br>✅ <code>"../../../events/newTask"</code> <br><br><span data-gb-custom-inline data-tag="emoji" data-code="274c">❌</span> <code>"src/events/newTask"</code><br><br>If your imports look correct, try following the steps below to clear stale build artifacts.</td></tr></tbody></table>

If you are encountering many TypeScript compilation errors that should be ignored, you can attempt a build that suppresses these types of errors with the `--skip-type-errors` flag:

```
para build --skip-type-errors
```



If you are encountering errors _after_ the TypeScript build succeeds, verify that your error is not caused by stale build artifacts:

* Delete the `dist/` folder.
* Delete the `tsconfig.tsbuildinfo` file.

These stale build artifacts may cause evaluation errors after deleting workflows or integrations.
