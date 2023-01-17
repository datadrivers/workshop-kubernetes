---
title: Manifests
permalink: /manifests
nav_order: 5
---

# Manifests

## Describing a Kubernetes object

When you create an object in Kubernetes, you must provide the object spec that describes its desired state, as well as some basic information about the object (such as a name). When you use the Kubernetes API to create the object (either directly or via kubectl), that API request must include that information as JSON in the request body. Most often, you provide the information to kubectl in a .yaml file. kubectl converts the information to JSON when making the API request.

Here's an example .yaml file that shows the required fields and object spec for a Kubernetes Deployment:

## Example

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2 # tells deployment to run 2 pods matching the template
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

## Required fields

In the .yaml file for the Kubernetes object you want to create, you'll need to set values for the following fields:

- apiVersion - Which version of the Kubernetes API you're using to create this object
- kind - What kind of object you want to create
- metadata - Data that helps uniquely identify the object, including a name string, UID, and optional namespace
- spec - What state you desire for the object

### Metadata

Every object kind MUST have the following metadata in a nested object field called "metadata":

- `namespace`: a namespace is a DNS compatible label that objects are subdivided into. The default namespace is 'default'. See the namespace docs for more.
- `name`: a string that uniquely identifies this object within the current namespace (see the identifiers docs). This value is used in the path when retrieving an individual object.
- `uid`: a unique in time and space value (typically an RFC 4122 generated identifier, see the identifiers docs) used to distinguish between objects with the same name that have been deleted and recreated

Every object SHOULD have the following metadata in a nested object field called "metadata":

- `resourceVersion`: a string that identifies the internal version of this object that can be used by clients to determine when objects have changed. This value MUST be treated as opaque by clients and passed unmodified back to the server. Clients should not assume that the resource version has meaning across namespaces, different kinds of resources, or different servers. (See concurrency control, below, for more details.)
- `generation`: a sequence number representing a specific generation of the desired state. Set by the system and monotonically increasing, per-resource. May be compared, such as for RAW and WAW consistency.
- `creationTimestamp`: a string representing an RFC 3339 date of the date and time an object was created
- `deletionTimestamp`: a string representing an RFC 3339 date of the date and time after which this resource will be deleted. This field is set by the server when a graceful deletion is requested by the user, and is not directly settable by a client. The resource will be deleted (no longer visible from resource lists, and not reachable by name) after the time in this field except when the object has a finalizer set. In case the finalizer is set the deletion of the object is postponed at least until the finalizer is removed. Once the deletionTimestamp is set, this value may not be unset or be set further into the future, although it may be shortened or the resource may be deleted prior to this time.
- `labels`: a map of string keys and values that can be used to organize and categorize objects
- `annotations`: a map of string keys and values that can be used by external tooling to store and retrieve arbitrary metadata about this object

### Spec

For objects that have a `spec`, you have to set this when you create the object, providing a description of the characteristics you want the resource to have: its desired state.

### Status

The `status` describes the current state of the object, supplied and updated by the Kubernetes system and its components. The Kubernetes control plane continually and actively manages every object's actual state to match the desired state you supplied.

For example: in Kubernetes, a Deployment is an object that can represent an application running on your cluster. When you create the Deployment, you might set the Deployment spec to specify that you want three replicas of the application to be running. The Kubernetes system reads the Deployment spec and starts three instances of your desired application--updating the status to match your spec. If any of those instances should fail (a status change), the Kubernetes system responds to the difference between spec and status by making a correction--in this case, starting a replacement instance.

For more information on the object spec, status, and metadata, see the Kubernetes API Conventions.


### Object Names and IDs

Each object in your cluster has a Name that is unique for that type of resource. Every Kubernetes object also has a UID that is unique across your whole cluster.

For example, you can only have one Pod named myapp-1234 within the same namespace, but you can have one Pod and one Deployment that are each named myapp-1234.

For non-unique user-provided attributes, Kubernetes provides labels and annotations.

---

Below are four types of commonly used name constraints for resources.

#### DNS Subdomain Names

Most resource types require a name that can be used as a DNS subdomain name as defined in RFC 1123. This means the name must:

- contain no more than 253 characters
- contain only lowercase alphanumeric characters, '-' or '.'
- start with an alphanumeric character
- end with an alphanumeric character

#### RFC 1123 Label Names

Some resource types require their names to follow the DNS label standard as defined in RFC 1123. This means the name must:

- contain at most 63 characters
- contain only lowercase alphanumeric characters or '-'
- start with an alphanumeric character
- end with an alphanumeric character

#### RFC 1035 Label Names

Some resource types require their names to follow the DNS label standard as defined in RFC 1035. This means the name must:

- contain at most 63 characters
- contain only lowercase alphanumeric characters or '-'
- start with an alphabetic character
- end with an alphanumeric character

#### Path Segment Names

Some resource types require their names to be able to be safely encoded as a path segment. In other words, the name may not be "." or ".." and the name may not contain "/" or "%".
