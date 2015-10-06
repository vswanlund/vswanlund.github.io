---
layout: page
title: Acts on Android
permalink: /tag-mobile-sdks/android/acts/
---

The "Act Now" functionality provides users with a means to respond to a merchant's act campaign. 
Some examples of Acts:
 <pre><i>"Book a test drive at a car dealership"
 "Request the campaign information pack from a charity"
 "Book a viewing of a painting at a gallery"</i></pre>

When a merchant sets up an Act campaign they specify what information they require from the user which is the presented through the SDK when they interact with a PowaTag trigger 

a user interacts with a PowaTag trigger and the resulting workflow is ‘Act now’ the user will be prompted to provide some personal information for a specific call to action. 

An Act can be to book a test drive. For this purpose the user may be required to provide personal details that would include their driving license details.
Another Act maybe to view a painting and this may only require some contact details.
Act campaigns are merchant-specific.

Consumer Experience:
Act Now can be triggered from any PowaTag trigger;
We present the user with information the merchant has supplied about their company, promotion or campaign.
The user then sees what information the merchant needs;

If mandatory information is missing, the user will be prompted to fill-in any gaps;
The user agrees to share the information with the merchant.

Client Integration:
The merchant must always choose a corresponding workflow to attach to their PowaTag.
When they choose the 'Act Now' workflow they must specify the data they require.
We send the information in these data fields to the merchant once the user provides and agrees to share them.

Title
First and last name
Email address
Mobile number
Default address (Line 1, Line 2, City, County, State, Postcode, Country)*
custom info


W
 Campaign is a particular charity or even a specific cause or event that the user can donate to. Donations can be made on a single-time or on a recurring monthly basis. If the merchant (charity) and consumer are both eligible for a tax-reclaim scheme, such as Gift Aid in the UK, this can be offered through the app.


 
   /**
     * The {@code ActManager} for the current application.
     */
    public static ActManager getInstance() {}

    /**
     * Act on an act campaign, submitting the required information in the transaction details.
     *
     * @param act The act campaign.
     * @param actTransactionDetails The act transaction details containing the default values to be submitted for the act campaign.
     * @param callback Callback to be invoked when the operation completes.
     */
    public void submitTransaction(@NonNull final Act act, @NonNull final ActTransactionDetails actTransactionDetails, @NonNull final PowaTagCallback<ActTransaction> callback) {}

    /**
     * Act on an act campaign, submitting the required information in the transaction details.
     * This method is blocking, do not use from the main thread.
     *
     * @param act The act campaign.
     * @param actTransactionDetails The act transaction details containing the default values to be submitted for the act campaign.
     * @throws PowaTagException if the request fails.
     */
    public ActTransaction submitTransaction(@NonNull final Act act, @NonNull final ActTransactionDetails actTransactionDetails)
            throws PowaTagException { }


    /**
     * Creates a new {@code Act} instance.
     *
     * @param actId The act ID.
     * @param name The name of the act.
     * @param merchant The act merchant.
     * @param actDataKeys List of act data keys.
     */
    public Act(@NonNull final String actId, @NonNull final String name, @NonNull final Merchant merchant, @NonNull final List<ActDataKey> actDataKeys) {    }

    /**
     * @return The act ID.
     */
    public String getActId() {    }

    /**
     * @return The name of the act.
     */
    public String getName() {   }

    /**
     * @return The merchant running the act.
     */
    public Merchant getMerchant() {    }

    /**
     * @return List of act data keys.
     */
    public List<ActDataKey> getActDataKeys() {  }
			
 
 
 
 
 
 
 
 
 
 
 
 
 
 
 
#Provide ability for users to perform acts on merchant Act campaigns.

To make a donation for a campaign create an invoice for the donation using the `CampaignManager`, then make a  [Payment]({{site.baseurl}}/tag-mobile-sdks/android/payments/) for that invoice.

<br />

# Creating an Invoice for a Campaign

Before creating an invoice you need to ensure the users [Profile]({{site.baseurl}}/tag-mobile-sdks/android/profile/) has all required information for the merchant.

1. Select a PaymentInstrument from the Profile that is accepted by the Merchant:

    <pre>List<PaymentMethodAlias> acceptedPaymentInstruments = ProfileManager.getInstance().getCurrentProfile().getAcceptedPaymentInstruments(merchant);
   PaymentInstrument paymentInstrument = acceptedPaymentInstruments.get(0);</pre>

2. Create an DonationInvoiceDetails to provide correct amount, payment instrument, gift aid address for crating an donation invoice. You can also specify if the donation repeats every month.

	<pre>DonationInvoiceDetails donationInvoiceDetails = new DonationInvoiceDetails(amount, repeated, paymentInstrument, giftAidAddress);

3. Use the CampaignManager to create an invoice for the correct amount:

    <pre>CampaignManager cm = CampaignManager.getInstance();
   cm.createInvoice(campaign, donationInvoiceDetails, new PowaTagCallback&lt;DonationInvoice&gt;() {
     public void onSuccess(DonationInvoice invoice) {
       Money amountToBeDonated = invoice.getAmount();
     }
     public void onError(PowaTagException exception) {
     }
   });</pre>

<br />

# Paying for a Donation Invoice

Once you have created an invoice for a campaign donation you can make a [Payment]({{site.baseurl}}/tag-mobile-sdks/android/payments/) for that invoice.

# Gift Aid

If the user is a UK taxpayer, has a UK address and confirms they are eligible for Gift Aid (e.g. through a checkbox) then you can provide the address when creating the invoice to allow registered charities to reclaim the tax on the donation.

# Repeated Donations

You can schedule a donation to be repeated every month when creating the invoice by setting `repeated = true`.
