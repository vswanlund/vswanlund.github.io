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
When a user interacts with the PowaTag trigger for the act campaign they are prompted to provide this information which is then sent to the merchant. 

WIP 
===

# Retrieve the Act

Obtain the act from the workflow and 
 
 	<pre>Act act = workflow.getAct();
	void initializeView(Act act) {
        LinearLayout actInformationContainer = (LinearLayout) findViewById(R.id.layout_act_information_container);
        for (ActDataKey actDataKey : act.getActDataKeys()) {
            ActField<?> actField = fieldGenerators.get(actDataKey.getType()).generate(actDataKey);
            actDataFields.put(actDataKey, actField);
            actInformationContainer.addView(actField.getView(), layoutParams);
        }
    }</pre>

# Present the Act Data Fields to the User


# Validate the Data Fields


# Submit the Act Transaction


   /**The {@code ActManager} for the current application.*/
    public static ActManager getInstance() {}

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
			
 