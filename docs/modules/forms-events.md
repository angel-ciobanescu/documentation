---
id: forms-events
title: Forms - Events
sidebar_label: Events
---

It is very important to understand when and and 

The Form Builder's `Events` tab allows you to define actions to be executed upon certain event steps in the Form's loading or submission

These actions are split in sections:

1. [`On Page Load`](#on-page-load) - what happens when the page is loaded.
2. [`On Preinit`](#on-preinit) - defines what happens before form fields get initialized.
3. [`On Init`](#on-init) - defines what happens after the form fields have been initialized with a value.
4. [`On Submit`](#on-submit) - what happens upon from submission (now defined for each individual button - see [*`Buttons`*](#buttons) section).
5. [`On Validation Failed`](#on-validation-failed) - defines a list of actions to be executed when validation fails.
6. [`Tab events`](#tab-events) - actions upon accessing/leaving a form tab.


To properly understand how and when each data type is loaded, please see the diagram below.

<img src="/img/forms-data-lifecycle.png" alt="forms-data-lifecycle.png"></img>

Accordingly, you can set the following data load events types (with specific implications) in your Form:

### `On Page Load`

These actions are executed right on the page load in the order you specify. This happens before all other events, and only once at the page load. By triggering a *reinit* page re-initialization) of this form will **not** trigger these actions! Note that contextual data generated by these actions will **not** persist. The main purpose of this action list is to compute conditional redirects (i.e. conditions).

### `On Preinit`

These actions are executed in the order you specify before form fields are initialized. Use it to load data the fields depend on.

Note that contextual data generated by these actions will **not** persist. This means that the values will only be loaded at the Preinit phase and cannot be used contextually afterwards.

As an example, you can use the context tokens in the *Conditions* of controls or in their default values, but you can't use them in the *Condition* of the Actions attached to buttons, because they will be executed later when the user clicks the button. You'll need to add the relevant actions to the button to load data in that context too.

### `On Init`

These actions are executed in the order you specify after the form fields have been initialized with a value. At this stage, you can reference fields by their `[FieldID]` token to get their values. 

Note that contextual data generated by these actions will **not** persist. This means that the values will only be loaded at the Preinit phase and cannot be used contextually afterwards.

### `On Submit`

The submission logic is defined for each individual button - see the "*`Buttons`*" section on the "***Main Menu and Usage***" page.

### `On Validation Failed`

Define a list of actions to be executed when the form validation fails. Actions will be executed in the specified order. The action's order can be modified by drag-and-drop.

### `Tab events`

Controls events relating to the tabs of your form. Define actions for tab access and tab exit.

- **Use Tab loading animation** - general setting. Trigger the Tab loading animation from the Form. It disables the Form's own loading animation (set under the see the "*`Settings`*" section on the "***Main Menu and Usage***" page) when navigating between tabs.

- **On Tab Enter**

Define what happens upon opening a tab; you can load an action from the *Actions* library (see the <a href="https://learn.plantanapp.com/docs/faq" target="_blank">**`Actions`**</a> section). Just as for the other event types above, you can define specific fields for each action: `Description`, `Error Message` and `Condition`.

- **On Tab Leave**

Define what happens upon leaving a tab; you can load an action from the *Actions* library (see the <a href="https://learn.plantanapp.com/docs/faq" target="_blank">**`Actions`**</a> section). Just as for the other event types above, you can define specific fields for each action: `Description`, `Error Message` and `Condition`.

- Additionally, there are four specific, checkbox type settings for the "Tab Leave" action:

  * `Refresh tab state` - if active, enables all tabs' conditions to be reevaluated when a Tab is changed.
  * `Ignore Validation` - enables *`Forms`* to avoid validation (both client and server side).
  * `Ignore TabLeave` - if activated, the actions will not be re-executed twice if the form has not been changed.
  * `Save To Reports` - enables *`Forms`* to save data to reports table.

:::tip

After you **`Save`** your changes, make sure that you also hit the "`🗘`" (*Refresh*) button to be able to see them in the Form you've created/modified.

:::

## Events Actions

The `Events` are action based - i.e. you can load an action from the *Actions* library (see the <a href="https://learn.plantanapp.com/docs/faq" target="_blank">**`Actions`**</a> section). Specific to Events' actions are three distinctive fields:

| Field | Description and information |
|---|---|
|*Description*|A text description for the action to help you identify its purpose (optional).|
|*Error Message*|Define a specific error message to be shown if an error occurs for the action. If left empty, the raw error message will be shown. This field supports Tokens.|
|*Condition*|Write a <a href="https://en.wikipedia.org/wiki/Boolean_expression" target="_blank">boolean expression</a> to determine if this action will execute. Use it to enable or disable actions programmatically. For example, you can enable a `ShowError` action only if an error occurs when you parsed a response from a web service.|