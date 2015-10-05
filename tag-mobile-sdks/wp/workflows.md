---
layout: page
title: Workflows on Windows Phone
permalink: /tag-mobile-sdks/wp/workflows/
---

A workflow defines the action(s) an application should offer the user for a particular tag, such as purchasing a product or claiming a coupon.

The workflow also includes the information required to display the actions (such as the product information).

After detecting a tag with one of the triggers use `WorkflowManager` to retrieve the workflow information for that tag.

The workflow information will contain the data necessary to integrate with the action SDK components (for instance through `BasketManager` and `Baskets` for a Product workflow).

The currently supported workflows are:

* Product
* Basket
* Campaign
* Act

<br />

# Determine the Workflow Type

1. Use the WorkflowType `AsXyzWorkflow` methods to convert the generic workflow object to the correct workflow subclass:

    <pre>switch (workflow.WorkflowType) {
     case Product:
       ProductWorkflow productWorkflow = WorkflowType.AsProductWorkflow(workflow);
       Product product = productWorkflow.Product;
       break;
     case Basket:
       TemporaryBasketWorkflow basketWorkflow = WorkflowType.AsBasketWorkflow(workflow);
       TemporaryBasket basket = basketWorkflow.Basket;
       break;
     case Campaign:
       CampaignWorkflow campaignWorkflow = WorkflowType.AsCampaignWorkflow(workflow);
       Campaign campaign = campaignWorkflow.Campaign;
       break
     case Act:
       ActWorkflow actWorkflow = WorkflowType.AsActWorkflow(workflow);
       Act act = actWorkflow.Campaign;
       break;	   
   }</pre>

<br />

# Retrieve a Workflow

1. Retrieve an instance of `WorkflowManager`:

    <pre>WorkflowManager wm = WorkflowManager.GetInstance();</pre>

2. Request the workflow information for a tag:

    <pre>Workflow workflow = await wm.GetWorkflow(tag);
   switch (workflow.WorkflowType) {
     ...
   }
   </pre>

<br />

# Workflow Types

**[Product]({{site.baseurl}}/tag-mobile-sdks/wp/products/)**<br />
Single product, that can be purchased immediately or added to a basket for later.

**[Basket]({{site.baseurl}}/tag-mobile-sdks/wp/baskets/)**<br />
TemporaryBasket containing a fixed set of items that can be purchased.

**[Campaign]({{site.baseurl}}/tag-mobile-sdks/wp/campaigns/)**<br />
Charity donation campaign, one time or recurring.

**[Act]({{site.baseurl}}/tag-mobile-sdks/wp/acts/)**<br />
Custom user information required to act on a merchant's act campaign.