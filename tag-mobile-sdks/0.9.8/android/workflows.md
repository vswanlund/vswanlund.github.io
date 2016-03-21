---
layout: page
title: Workflows on Android
permalink: /tag-mobile-sdks/0.9.8/android/workflows/
---

A workflow defines the action(s) an application should offer the user for a particular tag, such as purchasing a product or claiming a coupon.

The workflow also includes the information required to display the actions (such as the product information).

After detecting a tag with one of the [triggers]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/triggers/) use the `WorkflowManager` to retrieve the workflow information for the tag.

The workflow information will contain the data necessary to integrate with the action SDK components (for instance through `BasketManager` and `Baskets` for a Product workflow).



# Workflow Types

The currently supported workflow types are:

**[Product]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/products/)**<br />
Retrieve a single product, that can be purchased immediately or added to a basket for later.

**[Basket]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/baskets/)**<br />
TemporaryBasket containing a fixed set of items that can be purchased.

**[Appeal]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/appeal/)**<br />
A one-time or recurring donation.

**[Act]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/acts/)**<br />
Custom user information required to act on a merchant's call to action.

**[POS Basket]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/posbasket/)**<br />
Purchase of products at a Point Of Service.

**[Catalog]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/catalog/)**<br />
Allows the user to retrieve a catalog of products to review, select and checkout.

<br />

# Determine the Workflow Type

1. Use the `WorkflowType.asXyzWorkflow` methods to convert the generic workflow object to the correct workflow subclass:

<pre>switch (workflow.getWorkflowType()) {
 case PRODUCT:
   ProductWorkflow productWorkflow = WorkflowType.asProductWorkflow(workflow);
   Product product = productWorkflow.getProduct();
   break;
 case BASKET:
   TemporaryBasketWorkflow basketWorkflow = WorkflowType.asBasketWorkflow(workflow);
   TemporaryBasket basket = basketWorkflow.getBasket();
   break;
 case CAMPAIGN:
   CampaignWorkflow campaignWorkflow = WorkflowType.asCampaignWorkflow(workflow);
   Campaign campaign = campaignWorkflow.getCampaign();
   break;
 case ACT:
   ActWorkflow actWorkflow = WorkflowType.asActWorkflow(workflow);
   Act act = actWorkflow.getAct();
   break;
 case POS_BASKET:
   PosBasketWorkflow posBasketWorkflow = WorkflowType.asPosBasketWorkflow(workflow);
   PosBasket posBasket = posBasketWorkflow.getPosBasket();
   break;
 case CATALOG:
   CatalogWorkflow catalogWorkflow = WorkflowType.asCatalogWorkflow(workflow);
   Catalog catalog = catalogWorkflow.getCatalog();
   break;	   
}</pre>


<br />

# Retrieve a Workflow

1. Retrieve an instance of `WorkflowManager`:

<pre>WorkflowManager workflowManager = ManagerFactory.getInstance().getWorkflowManager();</pre>

2. Request the workflow information for a tag:

<pre>workflowManager.getWorkflow(tag, new PowaTagCallback&lt;Workflow&gt;() {
 public void onSuccess(Workflow workflow) {
   switch (workflow.getWorkflowType()) {
	 ...
   }
 }
 public void onError(PowaTagException exception) {
 }
});</pre>

The synchronous version of the <code>getWorkflow</code> method should not be used in the main thread to avoid performance issues

<code>Workflow workflow = workflowManager.getWorkflow(tag);</code>
	
<br />  
	

This can also be done using RxJava:
	
<pre>RxWorkflowManager workflowManager = RxManagerFactory.getInstance().getWorkflowManager();
workflowManager.getWorkflow(tag).subscribe(new Subscriber&lt;Workflow&gt;() {
	@Override
	public void onCompleted() {
	} 
	@Override
	public void onError(Throwable e) {
	}

	@Override
	public void onNext(Workflow workflow) {
		switch (workflow.getWorkflowType()) {
		...
		}
	}
});  </pre>

<br />