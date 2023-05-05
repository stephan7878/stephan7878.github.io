---
layout: post
title:  "The Azure Resource Explorer"
author: "Stephan Bester"
date:   2023-05-05 10:08:00 +0200
categories: azure
---

![arm-explorer]({{ "/assets/2023-05-05-arm-explorer.png" | relative_url }}){: width="5%" style="float: left; margin-right: 1em;" }
The [Azure Resource Explorer][resource-exp] is great tool that you can use to execute queries on the Azure Resource Management API's directly from your browser against your own subscriptions. This is a great way to discover the API's that are available and it provides you with both the REST queries and Ansible samples for easy programatic use or automation!

### Prerequisites

- Access to an Azure subscription  

If you do not have your own Azure subscription, you can always follow along with an Azure sandbox. Activate a sandbox and deploy a virtual machine using the [Exercise - Create a VM using the Azure portal][create-a-vm] on Microsoft Learn.

### Getting Started

From your browser you can access the Azure Resource Explorer by navigating to [resources.azure.com][resource-exp], or from within the [Azure Portal][portal] you can search for the Resource Explorer to access the [Resource Explorer Blade][resource-exp-blade].

![resource-exp]({{ "/assets/2023-05-05-resource-exp.png" | relative_url }})

![resource-exp-blade]({{ "/assets/2023-05-05-resource-exp-blade.png" | relative_url }})

Note that not all features are available from within the portal.

On the left you can expand the tree view to generate various queries within your subscription. When accessing the `providers` view, you are generating a subscription-wide query for a specific type of resource. For instance, retrieve all disks within the subscription by expanding:

```txt
|-- subscriptions
|   |-- Concierge Subscription
|   |   |-- providers
|   |   |   |-- Microsoft.Compute
|   |   |   |   |-- disks
```

![re-providers-disk]({{ "/assets/2023-05-05-re-providers-disk.png" | relative_url }})

The resources are returned as JSON within a value array. Notice that the corrosponding GET query for the API is also displayed.

We can also query for all resources within a scope, for instance all resources within a specific resource group.

```txt
|-- subscriptions
|   |-- Concierge Subscription
|   |   |-- resourceGroups
|   |   |   |-- YOUR-RESOURCE-GROUP
|   |   |   |   |-- resources
```

![re-resources]({{ "/assets/2023-05-05-re-resources.png" | relative_url }})

Notice that there is also an Ansible tab, which generates the corresponding Ansible tasks that will perform the same query.

![re-resources-ansible]({{ "/assets/2023-05-05-re-resources-ansible.png" | relative_url }})

We can also combine the two concepts, querying for specific types within a specific resource group. Let's see all virtual machines within the resource group.

```txt
|-- subscriptions
|   |-- Concierge Subscription
|   |   |-- resourceGroups
|   |   |   |-- YOUR-RESOURCE-GROUP
|   |   |   |   |-- providers
|   |   |   |   |   |-- Microsoft.Compute
|   |   |   |   |   |   |-- virtualMachines
```

![re-virtualMachines]({{ "/assets/2023-05-05-re-virtualMachines.png" | relative_url }})

### Conclusion

The Azure Resource Explorer is a great tool to navigate the Azure Resource Management APIs with plenty of possibilities for automation. Also check out my previous post on [Getting Started with the Azure Resource Explorer]({% post_url 2023-05-03-getting-started-with-the-azure-resource-graph %}) for more ways to discover your Azure resources.

[create-a-vm]: https://learn.microsoft.com/en-gb/training/modules/intro-to-azure-virtual-machines/3-create-a-vm
[resource-exp]: https://resources.azure.com/
[portal]: https://portal.azure.com
[resource-exp-blade]: https://portal.azure.com/#view/HubsExtension/ArmExplorerBlade