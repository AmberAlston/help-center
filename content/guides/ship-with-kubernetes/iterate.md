---
date: "2018-01-30T04:02:20Z"
title: "Iterating and Updating"
description: "A guide to walk you through iterating and updating a Kubernetes release in Replicated"
weight: "11003"
categories: [ "Kubernetes Guide" ]
index: "guides/kubernetes"
type: "chapter"
gradient: "kubernetes"
icon: "replicatedKubernetes"
---

# Iterate and Delivering Updates

This guide will walk you through making a change and delivering an update to an application after it's been deployed. It's assumed you have the environment from parts 1 and 2 of this guide ([creating a release](../create-release) and [installing](../install)). If you haven't completed these guides, head back and finish them first.

Now that we have a Kubernetes cluster running, a common task is to deliver updates. Let's change the number of nginx replicas to show how to deliver an update.

{{< linked_headline "Create a New Release" >}}

On the Releases page of the [Vendor Portal](https://vendor.replicated.com), click the Create Release link on top. Once again, you'll be taken to a YAML editor that shows the contents of the most recently created release. This gives us everything we've done so far, and our task now is to only write the changes needed to increase the number of nginx replicas.

{{< linked_headline "Change Nginx Replicas" >}}

In the release YAML, find the nginx image to change. The line is in the `deployment.yaml` file and looks like:

```yaml
replicas: 1
```

Change the number to `2` or more and that is all you have to do. For there to be a new release there needs to be some change, no matter now small.

{{< linked_headline "Save and Promote the Release" >}}

Following the same process we did before, click the Save Release button, go back one screen and click Promote next to the newly created Sequence 2. Choose the Unstable branch again to promote this new release. That's all that's needed to deliver an update to a channel. Now, any license installed from the "Unstable" channel will start with this new release, and any installation already running will be prompted to update to the new release.

{{< linked_headline "Update the Test Server" >}}

To install and test this new release, we need to connect to the Admin Console dashboard on port :8800 using a web browser. At this point, it will likely show that our test application is Up To Date and that No Updates Are Available. Replicated will  check for new updates about every five hours but we can force Replicated to check now and not wait for the next interval.

In the Application or Version History tab click on the Check For Updates button. On the version history page the faded "Deployed" button should become active and say "Deploy." In addition it should say how many files were changed and how many lines are different. You can click on that to view what has changed in the yaml.


![View Update](/images/guides/kubernetes/view-update.png)
[CHANGE THIS]

Clicking the Deploy button will apply the new YAML which will change the number of nginx replicas. This should only take a few seconds to deploy.

Next, head to the [Kubernetes scheduler documentation](/docs/kubernetes/getting-started) to learn how to prepare your application to deploy on Replicated with Kubernetes.
