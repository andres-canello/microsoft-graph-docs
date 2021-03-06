---
title: "People component in the Microsoft Graph Toolkit"
description: "You can use the `mgt-people` web component to display a group of people or contacts by using their photos or initials."
localization_priority: Normal
author: nmetulev
---

# People component in the Microsoft Graph Toolkit

You can use the `mgt-people` web component to display a group of people or contacts by using their photos or initials. By default, it will display the most frequent contacts for the signed in user.

This component uses multiple [mgt-person](./person.md) controls, but it can be bound to a set of people descriptors. If there are more people to display than the `show-max` value, a number will be added to indicate the number of additional contacts.

## Example

[jsfiddle example](https://jsfiddle.net/metulev/az6pqy2r/)

```html
<mgt-people></mgt-people>
```

![mgt-people](./images/mgt-people.png)

## Properties

By default, the `mgt-people` component fetches events from the `/me/people` endpoint with the `personType/class eq 'Person'` filter to display frequently contacted users. You can use several properties to change this behavior.

| Property | Attribute | Description |
| --- | --- | --- |
| `showMax` | `show-max` | Indicate the maximum number of people to show. Default value is 3. |
| `people` | `people` | An array of people to get or set the list of people rendered by the component. Use this property to access the people loaded by the component. Set this value to load your own people. |

The following example sets the maximum number of people to show.

```html
<mgt-people
  show-max="4">
</mgt-people>
```

## CSS custom properties

The `mgt-people` component defines the following CSS custom properties.

```css
mgt-people {
  --list-margin: 8px 4px 8px 8px; /* Margin for component */
  --avatar-margin: 0 4px 0 0; /* Margin for each person */
}
```

## Templates

The `mgt-people` supports several [templates](../templates.md) that you can use to replace certain parts of the component. To specify a template, include a `<template>` element inside a component and set the `data-type` value to one of the following.

| Data type | Data context | Description |
| --- | --- | --- |
| `default` | `people`: list of person objects | The default template replaces the entire component with your own. |
| `person` | `person`: person object | The template used to render each person. |
| `overflow` | `people`: list of person objects <br> `max`: number of shown people <br> `extra`: number of extra people | The template used to render the number beyond the max to the right of the list of people. |
| `no-data` | No data context is passed | The template used when no people are available. |

The following examples shows how to use the `person` template.

```html
<mgt-people>
  <template>
    <ul><li data-for="person in people">
      <mgt-person person-query="{{ person.userPrincipalName }}"></mgt-person>
      <h3>{{ person.displayName }}</h3>
      <p>{{ person.jobTitle }}</p>
      <p>{{ person.department }}</p>
    </li></ul>
  </template>
</mgt-people>
```

## Microsoft Graph permissions

This component uses the following Microsoft Graph APIs and permissions:

| Resource | Permission/scope |
| - | - |
| [/me/people](https://docs.microsoft.com/en-us/graph/api/user-list-people?view=graph-rest-1.0) | `People.Read` |

## Authentication

The control uses the global authentication provider described in the [authentication documentation](./../providers.md).
