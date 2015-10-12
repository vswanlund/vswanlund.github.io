---
layout: page
title: Acts on Windows Phone
permalink: /tag-mobile-sdks/wp/acts/
---

The "Act Now" functionality provides users with a means to respond to a merchant's act campaign.
<p>Some examples of Acts:</p>
 - Book a test drive at a car dealership.
 - Request an information pack from a charity.
 - Book a viewing of a painting at an art gallery.

When a merchant creates an Act campaign they specify the information they require from the user which is then stored as a template on the server. 
When a user interacts with the PowaTag trigger for the act campaign they need to be prompted to provide this information which is then sent to the merchant. 

<br/>

# Retrieving the Act Data Keys

1. Get the act from the workflow. (see the [Workflow]({{site.baseurl}}/tag-mobile-sdks/wp/workflows) for more details):

	<pre>Act act = workflow.Act;</pre>
	
2. Get the act data keys:
	
	The data needed to display the custom field to the user is stored in <code>ActDataKey</code> 

	<pre>foreach (ActDataKey actDataKey in act.ActDataKeys)
	{
		// Retrieve the key identifier for this custom value.
		string key = actDataKey.Key;

		// Retrieve the display name of the custom value.
		string name = actDataKey.Name;

		// Retrieve the data type that must be returned to the SDK. Valid types are String, Timestamp, Email and Flag.
		ActDataType actDataType = actDataKey.Type;

		// Retrieve the optional predefined value to display to the user.
		string value = actDataKey.PredefinedValue;
 
		// Retrieve the flag indicating if this is an optional field.
		bool optional = actDataKey.IsOptional;
	}</pre>

<br/>
	
# Adding an Act Data Value

1. Create a <code>ActTransactionDetails</code>:

	<pre>ActTransactionDetails actTransactionDetails = new ActTransactionDetails();</pre>

2. Add the values supplied by the user for each <code>ActDataKey</code>:

	Values must be added for at least each mandatory act data key.
	
	<pre>// Add the user's value as a string
	 actTransactionDetails.AddActDataValue(actDataKey, userValueString);</pre>
	
<br/>	

# Removing an Act Data Value

1. To remove a stored user value:
	
	<pre> bool valueRemoved = actTransactionDetails.RemoveActDataValue(actDatakey);</pre>	
	
<br/>

# Removing All Act Data Values

1. To clear <code>ActTransactionDetails</code> of all act data values:
	
	<pre>actTransactionDetails.ClearActDataValues();</pre>	
	
<br/>

# Obtaining All Act Data Values

1. To obtain all act data values added to <code>ActTransActionDetails</code>:
	
	<pre>IReadOnlyDictionary<string, string> actDataValues = actTransactionDetails.ActDataValues;</pre>	
	
<br/>
		
# Submit the Act Transaction Details

1. Submit the act transaction details using the <code>ActManager</code>:
	
	<pre>ActManager actManager = ActManager.GetInstance();
	// submit the transaction and keep the transaction ID stored in actTransaction.
	ActTransaction actTransaction = await actManager.SubmitTransactionAsync(act, actTransactionDetails);</pre>
	
<br/>

# Useful Act Properties

1. The following methods can be used to obtian useful act information:

	<pre>// Get the ID of the act.
	String actId = act.ActId;
	
	// Get the name of the act.
	String actName = act.Name;
 
	// Get the merchant running the act.
	Merchant merchant = act.Merchant;
    
    // Get the List of act data keys.
	List<ActDataKey> actDataKeys = act.ActDataKeys;</pre>
