---
layout: post
title:  "Getting Started with the Azure Resource Graph"
author: "Stephan Bester"
date:   2023-05-03 12:15:00 +0200
categories: azure
---

![resource-graph-explorer]({{ "/assets/2023-05-03-resource-graph-explorer.png" | relative_url }}){: width="30%" style="float: left; margin-right: 1em;" }
The Azure Resource Graph is a very useful service which allows you to query your Azure resources from the Resource Graph Explorer within the [Azure Portal][portal], using [Kusto Query Langauge (KQL)][kql].

I recently used it on a project where we needed to inspect a complex Azure environment with many different Virtual Machines and Disks. In this blog post I will help you get started with the Resource Graph and share some very basic KQL queries!

### Prerequisites

- Access to an Azure subscription  

If you do not have your own Azure subscription, you can always follow along with an Azure sandbox. Activate a sandbox and deploy a virtual machine using the [Exercise - Create a VM using the Azure portal][create-a-vm] on Microsoft Learn.

### Getting Started

From the [Azure Portal][portal] navigate to the Resource Graph Explorer or follow this [link][rgexp].

Quering is simple, and you can view all resources by selecting all the data from the `resources` table. If you are familiar with SQL, check out this [SQL to Kusto cheat sheet][cheatsheet].

```kql
resources
```

![resources]({{ "/assets/2023-05-03-resources.png" | relative_url }})

Notice that this brings back all default columns. You can limit the columns in your selection by using the `project` keyword. I will also order the results by including an `order by` clause.

```kql
resources
| project name, resourceGroup, location
| order by resourceGroup asc
```

![project-orderby]({{ "/assets/2023-05-03-project-orderby.png" | relative_url }})

We can filter our results by using a `where` statement. We need to filter first, because you cannot apply a filter on a column not included in the projection. First we will filter on a specific resource group.

```kql
resources
| where resourceGroup == "<YOUR RESOURCE GROUP>"
| project name, location
```

![where]({{ "/assets/2023-05-03-where.png" | relative_url }})

We can also include all resource specific attributes by including the `properties` column. Notice that this brings back all properties as JSON. We want to look at Virtual Machines, so filter on `type`.

```kql
resources
| where type == "microsoft.compute/virtualmachines"
| project name, location, resourceGroup, properties
```

![properties]({{ "/assets/2023-05-03-properties.png" | relative_url }})

You can even access attributes within the properties JSON, like we do here with `vmSize`.

```kql
resources
| where type == "microsoft.compute/virtualmachines"
| project name, location, resourceGroup, vmSize=properties.hardwareProfile.vmSize
```

![vmSize]({{ "/assets/2023-05-03-vmSize.png" | relative_url }})

### Conclusion

As you can see, the Azure Resource Graph is a powerful way to query resources. With support for many [common operators][learn-common-operators], [aggregate functions][use-aggregation-functions], [table joins][join-data-from-multiple-tables] and [geospatial visualizations][create-geospatial-visualizations] you can easily create powerful queries to gain insights and vizualize the results.

### Useful links

- Azure Resource Graph
  - [Overview][resource-graph-overview]
  - [Get started][resource-graph-get-started]
  - [Documentation][resource-graph-docs]
- Kusto Query Langauge
  - [1 - Learn common operators][learn-common-operators]
  - [2 - Use aggregate functions][use-aggregation-functions]
  - [3 - Join data from multiple tables][join-data-from-multiple-tables]
  - [4 - Create geospatial visualizations][create-geospatial-visualizations]

[resource-graph-overview]: https://docs.microsoft.com/azure/governance/resource-graph/overview
[resource-graph-get-started]: https://docs.microsoft.com/azure/governance/resource-graph/first-query-portal
[resource-graph-docs]: https://docs.microsoft.com/azure/governance/resource-graph
[kql]: https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/
[create-a-vm]: https://learn.microsoft.com/en-gb/training/modules/intro-to-azure-virtual-machines/3-create-a-vm
[portal]: https://portal.azure.com
[rgexp]: https://portal.azure.com/#view/HubsExtension/ArgQueryBlade
[cheatsheet]: https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/sqlcheatsheet
[learn-common-operators]: https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/tutorials/learn-common-operators
[use-aggregation-functions]: https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/tutorials/use-aggregation-functions
[join-data-from-multiple-tables]: https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/tutorials/join-data-from-multiple-tables
[create-geospatial-visualizations]: https://learn.microsoft.com/en-us/azure/data-explorer/kusto/query/tutorials/create-geospatial-visualizations