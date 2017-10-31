# Module AppCluster

## Table of Contents

This list provides an overview of all types, values and functions exported from this module.  These are not necessarily defined in this module: in some cases, we also re-export items from other modules. When that is the case, we link to the appropriate definition.

<div id="lwdoc-toc-marker" style="display: hidden"></div>

-   Type [`App`](#type-app)

-   Function [`app`](#function-app)

-   Type [`AppCluster`](#type-appcluster)

-   Function [`new`](#function-new)

## Type App

An app is basically a docker image together with some parameters.  You can
deploy multiple apps in an [`AppCluster`](#type-appcluster).  For every app, the appropriate
resources (including a separate load balancer, security group...) will be
created.

    type App:
      | App
          name: String
          image: String
          port: Int
          memory: Int
          managedPolicies: List<ManagedPolicy>
          logGroupName: Optional<String>

### Constructor App

### Fields

-   `name` : [`String`](Ludwig.String.html)

-   `image` : [`String`](Ludwig.String.html)

-   `port` : [`Int`](Ludwig.Int.html)

-   `memory` : [`Int`](Ludwig.Int.html)

-   `managedPolicies` : [`List`](Ludwig.List.html)`<`[`ManagedPolicy`](Fugue.Core.AWS.IAM.html#type-managedpolicy)`>`

-   `logGroupName` : [`Optional`](Ludwig.Optional.html)`<`[`String`](Ludwig.String.html)`>`

## Function app

### Type

`fun{name:` [`String`](Ludwig.String.html)`,` `image:` [`String`](Ludwig.String.html)`,` `logGroupName:` [`Optional`](Ludwig.Optional.html)`<`[`String`](Ludwig.String.html)`>,` `port:` [`Optional`](Ludwig.Optional.html)`<`[`Int`](Ludwig.Int.html)`>,` `memory:` [`Optional`](Ludwig.Optional.html)`<`[`Int`](Ludwig.Int.html)`>,` `managedPolicies:` [`Optional`](Ludwig.Optional.html)`<`[`List`](Ludwig.List.html)`<`[`ManagedPolicy`](Fugue.Core.AWS.IAM.html#type-managedpolicy)`>>}` `->` [`App`](#type-app)

Constructor to create a new [`App`](#type-app).

### Arguments

-   `name`: [`String`](Ludwig.String.html)

    Descriptive name for the application.  Lowercase and hyphen is
    recommended.

-   `image`: [`String`](Ludwig.String.html)

    Name of the docker image.

-   `logGroupName`: [`Optional`](Ludwig.Optional.html)`<`[`String`](Ludwig.String.html)`>`

    CloudWatch log group name to send logs to.

-   `port`: [`Optional`](Ludwig.Optional.html)`<`[`Int`](Ludwig.Int.html)`>`

    Port on which your docker image listens.  Defaults to 8000.

-   `memory`: [`Optional`](Ludwig.Optional.html)`<`[`Int`](Ludwig.Int.html)`>`

    Amount of memory available to the image, in MB.  Defaults to 256.

-   `managedPolicies`: [`Optional`](Ludwig.Optional.html)`<`[`List`](Ludwig.List.html)`<`[`ManagedPolicy`](Fugue.Core.AWS.IAM.html#type-managedpolicy)`>>`

    Extra policies your docker image needs (e.g. SQS access).
    TODO: The use should be able to specify inline policies as well.

### Returns

[`App`](#type-app)

## Type AppCluster

    type AppCluster:
      cluster: Cluster
      services: List<Service>
      asg: AutoScalingGroup

### Fields

-   `cluster` : [`Cluster`](Fugue.Core.AWS.ECS.html#type-cluster)

-   `services` : [`List`](Ludwig.List.html)`<`[`Service`](Fugue.Core.AWS.ECS.html#type-service)`>`

-   `asg` : [`AutoScalingGroup`](Fugue.Core.AWS.AutoScaling.html#type-autoscalinggroup)

## Function new

### Type

`fun{name:` [`String`](Ludwig.String.html)`,` `network:` [`Network`](Fugue.AWS.Pattern.Network.html#type-network)`,` `apps:` [`List`](Ludwig.List.html)`<`[`App`](#type-app)`>,` `size:` [`Optional`](Ludwig.Optional.html)`<`[`Int`](Ludwig.Int.html)`>,` `keyName:` [`Optional`](Ludwig.Optional.html)`<`[`String`](Ludwig.String.html)`>}` `->` [`AppCluster`](#type-appcluster)

Create a new [`AppCluster`](#type-appcluster)

### Arguments

-   `name`: [`String`](Ludwig.String.html)

    Name of the cluster.  Using lowercase and hyphens is recommended.

-   `network`: [`Network`](Fugue.AWS.Pattern.Network.html#type-network)

    Network to deploy the cluster in.

-   `apps`: [`List`](Ludwig.List.html)`<`[`App`](#type-app)`>`

-   `size`: [`Optional`](Ludwig.Optional.html)`<`[`Int`](Ludwig.Int.html)`>`

    Number of instances in the network.  Defaults to the number apps +
    1.

-   `keyName`: [`Optional`](Ludwig.Optional.html)`<`[`String`](Ludwig.String.html)`>`

### Returns

[`AppCluster`](#type-appcluster)
