---
title: Labels
permalink: /labels
nav_order: 6
---

# Labels

- Labels are key/value pairs that are attached to objects, such as pods.
- Labels are intended to be used to specify identifying attributes of objects that are meaningful and relevant to users, but do not directly imply semantics to the core system.
- Labels can be used to organize and to select subsets of objects.
- Labels can be attached to objects at creation time and subsequently added and modified at any time.
- Each object can have a set of key/value labels defined. Each Key must be unique for a given object.

```yaml
"metadata": {
  "labels": {
    "key1" : "value1",
    "key2" : "value2"
  }
}
```

Labels allow for efficient queries and watches and are ideal for use in UIs and CLIs. Non-identifying information should be recorded using annotations.

## Label selectors

Unlike names and UIDs, labels do not provide uniqueness. In general, we expect many objects to carry the same label(s).

Via a label selector, the client/user can identify a set of objects. The label selector is the core grouping primitive in Kubernetes.

The API currently supports two types of selectors: equality-based and set-based. A label selector can be made of multiple requirements which are comma-separated. In the case of multiple requirements, all must be satisfied so the comma separator acts as a logical AND (&&) operator.

The semantics of empty or non-specified selectors are dependent on the context, and API types that use selectors should document the validity and meaning of them.

## Recommended Labels

You can visualize and manage Kubernetes objects with more tools than kubectl and the dashboard. A common set of labels allows tools to work interoperably, describing objects in a common manner that all tools can understand.

In addition to supporting tooling, the recommended labels describe applications in a way that can be queried.

The metadata is organized around the concept of an application. Kubernetes is not a platform as a service (PaaS) and doesn't have or enforce a formal notion of an application. Instead, applications are informal and described with metadata. The definition of what an application contains is loose.

Note: These are recommended labels. They make it easier to manage applications but aren't required for any core tooling.

Shared labels and annotations share a common prefix: app.kubernetes.io. Labels without a prefix are private to users. The shared prefix ensures that shared labels do not interfere with custom user labels.

| Key                          | Description                                                                      | Example      | Type   |
|------------------------------|----------------------------------------------------------------------------------|--------------|--------|
| app.kubernetes.io/name       | The name of the application                                                      | mysql        | string |
| app.kubernetes.io/instance   | A unique name identifying the instance of an application                         | mysql-abcxzy | string |
| app.kubernetes.io/version    | The current version of the application (e.g., a SemVer 1.0, revision hash, etc.) | 5.7.21       | string |
| app.kubernetes.io/component  | The component within the architecture                                            | database     | string |
| app.kubernetes.io/part-of    | The name of a higher level application this one is part of                       | wordpress    | string |
| app.kubernetes.io/managed-by | The tool being used to manage the operation of an application                    | helm         | string |
