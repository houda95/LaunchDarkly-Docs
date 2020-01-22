---
title: "Prerequisites"
excerpt: ""
---
## Overview
This topic explains how to use feature flag prerequisites to enable or disable features based on different states.
## Understanding flag prerequisite relationships
Prerequisites allow you to control feature dependencies in LaunchDarkly. You can make flags depend on other flags being enabled to take effect themselves, making them prerequisites to enable a feature.

For example, you have two flags that control read and write access to an API: `api_reads` and `api_writes`.  If you do not have read access to the API, you cannot see it, so you cannot write to it. You can set up `api_reads` as a prerequisite before `api_writes` is evaluated for a user by making sure `api_reads` is **On** and the user is seeing the `true` variation.

Manage prerequisites in the feature flag's Targeting tab:
[block:image]
{
  "images": [
    {
      "image": [
        "https://files.readme.io/e410d36-doc_pre.jpg",
        "doc_pre.jpg",
        2000,
        1125,
        "#f6f8f5"
      ],
      "caption": "The flag's Targeting tab with the Prerequisites section called out."
    }
  ]
}
[/block]
In the screenshot above, the `api_reads` flag is a prerequisite of the `api_writes` flag. To meet a prerequisite, the prerequisite flag must be **On**, and the user must receive the variation you specify. 

In this example, if a user receives the `false` variation of the `api_reads` flag, they will not be able to write to the API. The `api_writes` flag will not evaluate for them, because the prerequisites are not met.
<Callout intent="info">
  <Callout.Title>Don't worry about circular dependencies</Callout.Title>
   <Callout.Description>LaunchDarkly automatically prevents you from saving changes that would introduce circular dependencies between prerequisites. 
For example, you cannot make Flag A a prerequisite of Flag B and also make Flag B a prerequisite of Flag A.</Callout.Description>
</Callout>

<Callout intent="alert">
  <Callout.Title>Deleting flags with prerequisites</Callout.Title>
   <Callout.Description>You cannot remove a flag that is a prerequisite for other flags. You must remove the dependency before you can delete the prerequisite flag.</Callout.Description>
</Callout>