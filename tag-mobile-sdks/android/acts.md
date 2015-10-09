---
layout: page
title: Acts on Android
permalink: /tag-mobile-sdks/android/acts/
---

The "Act Now" functionality provides users with a means to respond to a merchant's act campaign.
<p>Some examples of Acts:</p>
 - Book a test drive at a car dealership.
 - Request an information pack from a charity.
 - Book a viewing of a painting at an art gallery.

When a merchant creates an Act campaign they specify the information they require from the user which is then stored as a template on the server. 
When a user interacts with the PowaTag trigger for the act campaign they need to be prompted to provide this information which is then sent to the merchant. 

# Retrieving the Act

1. Get the act from the workflow. (see the [Workflow]({{site.baseurl}}/tag-mobile-sdks/android/workflows) for more details)

	<pre>Act act = workflow.getAct();</pre>
	
2. Get the act data keys 
	
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
	
# Add values to the ActTransactionDetails
once all data has been obetained from the user and valided then its time to submit the act using the ActManager
	
	TO do this you need to create an actTransactionDetails object
	ActTransactionDetails actTransactionDetails = new ActTransactionDetails();
	
# Submit the Act Transaction Details

	once all data has been obetained from the user and valided then its time to submit the act using the ActManager
	
	TO do this you need to create an actTransactionDetails object
	ActTransactionDetails actTransactionDetails = new ActTransactionDetails();
	
	
	actmangaer actManger = Actmanager.getinstance();
	actManger.submitTransaction(act)
    /** Act on an act campaign, submitting the required information in the transaction details.
     * @param act The act campaign.
     * @param actTransactionDetails The act transaction details containing the default values to be submitted for the act campaign.     */
    public void submitTransaction(@NonNull final Act act, @NonNull final ActTransactionDetails actTransactionDetails, @NonNull final PowaTagCallback<ActTransaction> callback) {}

    /**Act on an act campaign, submitting the required information in the transaction details.
     * This method is blocking, do not use from the main thread.
     *
     * @param act The act campaign.
     * @param actTransactionDetails The act transaction details containing the default values to be submitted for the act campaign.     */
    public ActTransaction submitTransaction(@NonNull final Act act, @NonNull final ActTransactionDetails actTransactionDetails)
            throws PowaTagException { }


    /**Creates a new {@code Act} instance.     *
     * @param actId The act ID.
     * @param name The name of the act.
     * @param merchant The act merchant.
     * @param actDataKeys List of act data keys.     */
    public Act(@NonNull final String actId, @NonNull final String name, @NonNull final Merchant merchant, @NonNull final List<ActDataKey> actDataKeys) {    }

    /**     * @return The act ID.     */
    public String getActId() {    }

    /**     * @return The name of the act.     */
    public String getName() {   }

    /**     * @return The merchant running the act.     */
    public Merchant getMerchant() {    }

    /**     * @return List of act data keys.     */
    public List<ActDataKey> getActDataKeys() {  }
			
 