---
layout: page
title: Workflows on iOS
permalink: /tag-mobile-sdks/0.9.8/ios/workflows/
---

A workflow defines the action(s) an application should offer the user for a particular tag, such as purchasing a product or claiming a coupon.

The workflow also includes the information required to display the actions (such as the product information).

After detecting a tag with one of the [triggers]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/triggers/) use the `PTKWorkflowManager` to retrieve the workflow information for the tag.

The workflow information will contain the data necessary to integrate with the action SDK components (for instance through `PTKBasketManager` and `PTKBaskets` for a product workflow).



# Workflow Types

The currently supported workflow types are:

**[Product]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/products/)**<br />
Retrieve a single product, that can be purchased immediately or added to a basket for later.

**[Basket]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/baskets/)**<br />
TemporaryBasket containing a fixed set of items that can be purchased.

**[Appeal]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/appeal/)**<br />
A one-time or recurring donation.

**[Act]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/acts/)**<br />
Custom user information required to act on a merchant's call to action.

**[POS Basket]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/posbasket/)**<br />
Purchase of products at a Point Of Service.

**[Catalog]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/catalog/)**<br />
Allows the user to retrieve a catalog of products to review, select and checkout.

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
     case PTKWorkflowTypeAppeal:
       PTKCampaignWorkflow *campaignWorkflow = [PTKWorkflow asCampaignWorkflow:workflow];
       PTKCampaign *campaign = campaignWorkflow.campaign;
       break;
	case PTKWorkflowTypeAct:
       PTKActWorkflow *actWorkflow = [PTKWorkflow asActWorkflow:workflow];
       PTKAct *act = actWorkflow.act;
       break;
	case PTKWorkflowTypePOSBasket:
       PTKPOSBasketWorkflow *posBasketWorkflow = [PTKWorkflow asPOSBasketWorkflow:workflow];
       PTKPOSBasket *posBasket = posBasketWorkflow.posBasket;
       break;
	case PTKWorkflowTypeCatalog:
       PTKCampaignWorkflow *campaignWorkflow = [PTKWorkflow asCampaignWorkflow:workflow];
       PTKCatalog *catalog = campaignWorkflow.catalog;
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