---
layout: page
title: Act Now on Android
permalink: /tag-mobile-sdks/0.9.8/android/acts/
---

The "Act Now" functionality provides users with a means to respond to a merchant's "call to action".
<p>Some examples of Acts:</p>
 - Book a test drive at a car dealership.
 - Request an information pack from a charity.
 - Book a viewing of a painting at an art gallery.

When a merchant creates an "Act Now" they specify the information they require from the user which is then stored as a template on the server and link it to an Act [workflow]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/workflows).
When a user interacts with the PowaTag [trigger]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/triggers) associated with the workflow they need to be prompted to provide the required.

<br/>

# Retrieving the Act Data Keys

1. Get the act from the workflow. (see the [Workflow]({{site.baseurl}}/tag-mobile-sdks/0.9.8/android/workflows) for more details):

	<pre>Act act = workflow.getAct();</pre>

2. Get the act data keys:

	The data needed to display the custom field to the user is stored in <code>ActDataKey</code>

	<pre>for (ActDataKey actDataKey : act.getActDataKeys()) {
		// Retrieve the key identifier for this custom value
		String key = actDataKey.getKey();

		// Retrieve the display name of the custom value
		String name = actDataKey.getName();

		// Retrieve the data type the must be returned to the SDK. valid types are String, Timestamp, Email,Flag
		ActDataType actDataType = actDataKey.getType();

		// Retrieve the optional predefined value to display to the user
		String value = actDataKey.getPredefinedValue();

		// Retrieve the flag indicating if this is an optional field
		boolean optional = actDataKey.isOptional();
	}</pre>

<br/>

# Adding an Act Data Value

1. Create a <code>ActTransactionDetails</code>:

	<pre>ActTransactionDetails actTransactionDetails = new ActTransactionDetails();</pre>

2. Add the values supplied by the user for each <code>ActDataKey</code>:

	Values must be added for at least each mandatory act data key.

	<pre>// Add the user's value as a string
	actTransactionDetails.addActDataValue(actDataKey, userValueString);</pre>

<br/>

# Removing an Act Data Value

1. To remove a stored user value:

	<pre>boolean valueRemoved = actTransactionDetails.removeActDataValue(actDatakey);</pre>

<br/>

# Removing All Act Data Values

1. To clear <code>ActTransactionDetails</code> of all act data values:

	<pre>actTransactionDetails.clearActDataValues();</pre>

<br/>

# Obtaining All Act Data Values

1. To obtain all act data values added to <code>ActTransActionDetails</code>:

	<pre>Map<String, String> actDataValues = actTransactionDetails.getActDataValues();</pre>

<br/>

# Submit the Act Transaction Details

1. Submit the act transaction details using the <code>ActManager</code>:

	<pre>ActManager actManager = ManagerFactory.getInstance().getActManager();
	// submit the transaction and keep the transaction ID stored in actTransaction
	ActTransaction actTransaction = actManager.submitTransaction(act, actTransactionDetails,new PowaTagCallback&lt;ActTransaction&gt;());  </pre>  

<br/>  

This can also be done using RxJava:
	
<pre>RxActManager actManager = RxManagerFactory.getInstance().getActManager();
actManager.submitTransaction(act,actTransactionDetails).subscribe(new Subscriber&lt;ActTransaction&gt;() {
	@Override
	public void onCompleted() {
	}

	@Override
	public void onError(Throwable e) {
	}

	@Override 
	public void onNext(ActTransaction actTransaction) {
	}
});
</pre>

<br/>


# Useful Act Methods

1. The following methods can be used to obtian useful act information:

	<pre>// Get the ID of the act.
	String actId = act.getActId();

	// Get the name of the act.
	String actName = act.getName();

	// Get the merchant running the act.
	Merchant merchant = act.getMerchant();

    // Get the List of act data keys.
	List<ActDataKey> actDataKeys = act.getActDataKeys();</pre>


