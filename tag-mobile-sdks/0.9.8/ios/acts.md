---
layout: page
title: Act Now on iOS
permalink: /tag-mobile-sdks/0.9.8/ios/acts/
---

The "Act Now" functionality provides users with a means to respond to a merchant's "call to action".
<p>Some examples of Acts:</p>
 - Book a test drive at a car dealership.
 - Request an information pack from a charity.
 - Book a viewing of a painting at an art gallery.

When a merchant creates an "Act Now" they specify the information they require from the user which is then stored as a template on the server and link it to an Act [Workflow]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/workflows).
When a user interacts with the PowaTag [trigger]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/triggers) associated with the workflow they need to be prompted to provide the required.

<br/>

# Retrieving the Act Data Keys

1. Get the act from the workflow. (see the [Workflow]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/workflows) for more details):

	<pre>PTKAct *act = workflow.act;</pre>

2. Get the act data keys:

	The data needed to display the custom field to the user is stored in <code>PTKActDataKey</code>

	<pre>for (PTKActDataKey actDataKey : act.actDataKeys) {
	// Retrieve the key identifier for this custom value
	NSString *key = actDataKey.key;

	// Retrieve the display name of the custom value
	NSString *name = actDataKey.name;

	// Retrieve the data type the must be returned to the SDK. valid types are String, Timestamp, Email,Flag
	PTKActDataType actDataType = actDataKey.type;

	// Retrieve the optional predefined value to display to the user
	NSString *value = actDataKey.predefinedValue;

	// Retrieve the flag indicating if this is an optional field
	BOOL optional = actDataKey.optional;
 }</pre>

<br/>

# Adding an Act Data Value

1. Create a <code>PTKActTransactionDetails</code>:

	<pre>PTKActTransactionDetails *actTransactionDetails = [PTKActTransactionDetails actTransactionDetails];</pre>

2. Add the values supplied by the user for each <code>PTKActDataKey</code>:

	Values must be added for at least each mandatory act data key.

	<pre>// Add the user's value as a string
	[actTransactionDetails addActDataValueForKey:actDataKey value:userValueString];</pre>

<br/>

# Removing an Act Data Value

1. To remove a stored user value:

	<pre>BOOL valueRemoved = [actTransactionDetails removeActDataValue:actDatakey];</pre>

<br/>

# Removing All Act Data Values

1. To clear <code>PTKActTransactionDetails</code> of all act data values:

	<pre>[actTransactionDetails clearActDataValues];</pre>

<br/>

# Obtaining All Act Data Values

1. To obtain all act data values added to <code>PTKActTransActionDetails</code>:

	<pre>NSDictionary *actDataValues = [actTransactionDetails actDataValues];</pre>

<br/>

# Submit the Act Transaction Details

1. Submit the act transaction details using the <code>PTKActManager</code>:

	<pre>PTKActManager *actManager = [PTKActManager sharedManager];
	// submit the transaction and keep the transaction ID stored in actTransaction
	[actManager submitTransactionWithAct:act transactionDetails:actTransactionDetails completion:^(PTKActTransaction *actTransaction, NSError *error)];</pre>


<br/>

# Useful Act Methods

1. The following methods can be used to obtian useful act information:

	<pre>// Get the ID of the act.
	NSString *actId = act.actId;

	// Get the name of the act.
	NSString *actName = act.name;

	// Get the merchant running the act.
	PTKMerchant *merchant = act.merchant;

	// Get the List of act data keys.
	NSArray *actDataKeys = act.actDataKeys;</pre>


