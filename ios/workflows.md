---
layout: page
title: Workflows on iOS
permalink: /tag-mobile-sdks/ios/workflows/
---

A workflow defines the action(s) an application should offer the user for a particular tag, such as purchasing a product or claiming a coupon.

The workflow also includes the information required to display the actions (such as the product information).

After detecting a tag with one of the triggers use `PTKWorkflowManager` to retrieve the workflow information for that tag.

The workflow information will contain the data necessary to integrate with the action SDK components (for instance through `BasketManager` and `Baskets` for a Product workflow).

The currently supported workflows are:

* Product
* Basket
* Campaign

<br />

# Determine the Workflow Type

1. Use the WorkflowType `asXyzWorkflow` methods to convert the generic workflow object to the correct workflow subclass:

    <pre>switch (workflow.workflowType) {
     case PTKWorkflowTypeProduct:
       PTKProductWorkflow *productWorkflow = [PTKWorkflow asProductWorkflow:workflow];
       PTKProduct *product = productWorkflow.product;
       break;
     case PTKWorkflowTypeBasket:
       PTKTemporaryBasketWorkflow *basketWorkflow = [PTKWorkflow asBasketWorkflow:workflow];
       PTKTemporaryBasket *basket = basketWorkflow.basket;
       break;
     case PTKWorkflowTypeCampaign:
       PTKCampaignWorkflow *campaignWorkflow = [PTKWorkflow asCampaignWorkflow:workflow];
       PTKCampaign *campaign = campaignWorkflow.campaign;
       break;
   }</pre>

# Retrieve a Workflow

1. Retrieve an instance of `PTKWorkflowManager`:

    <pre>PTKWorkflowManager *wm = [PTKWorkflowManager sharedManager]</pre>

2. Request the workflow information for a tag:

    <pre>[wm workflowForTag:tag completion:^(PTKWorkflow *workflow, NSError *error) {
     switch (workflow.workflowType) {
       ...
     }
   });</pre>

<br />

# Workflow Types

**[Product]({{site.baseurl}}/tag-mobile-sdks/ios/products/)**<br />
Single product, that can be purchased immediately or added to a basket for later.

**[Basket]({{site.baseurl}}/tag-mobile-sdks/ios/baskets/)**<br />
TemporaryBasket containing a fixed set of items that can be purchased.

**[Campaign]({{site.baseurl}}/tag-mobile-sdks/ios/campaigns/)**<br />
Charity donation campaign, one time or recurring.
