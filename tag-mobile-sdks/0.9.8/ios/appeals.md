---
layout: page
title: Appeals on iOS
permalink: /tag-mobile-sdks/0.9.8/ios/appeals/
---

An Appeal is a particular charity or even a specific cause or event that the user can donate to. Donations can be made on a once-off or recurring monthly basis. If the merchant (charity) and consumer are both eligible for a tax-reclaim scheme, such as Gift Aid in the UK, this can be offered through the app.

To make a donation the user will interact with a PowaTag [trigger]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/triggers/) which is associated with the appeal and using the SDK you will obtain the  [workflow]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/workflows/). 
Then create a donation invoice using the `CampaignManager`, then make a [Payment]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/payments/) for the invoice.

<br />

# Creating an Invoice for a Appeal

Before creating an invoice you need to ensure the users [Profile]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/profile/) has all required information for the merchant.

1. Select a PaymentInstrument from the Profile that is accepted by the Merchant:

	<pre>NSArray *acceptedPaymentInstruments = [[ProfileManager sharedManager].currentProfile acceptedPaymentInstrumentsForMerchant(merchant)];
	PTKPaymentInstrument *paymentInstrument = acceptedPaymentInstruments.firstObject;</pre>

2. Create donation invoice details object with all necessary data:

	<pre>PTKDonationInvoiceDetails *donationInvoiceDetails = [PTKDonationInvoiceDetails donationInvoiceDetailsWithAmount:amount isRepeated:isRepeated paymentInstrument:paymentInstrument giftAidAddress:giftAidAddress];</pre>

3. Use the CampaignManager to create an invoice for the correct amount, you can also specify if the donation repeats every month and gift aid address:

    <pre>PTKCampaignManager *cm = [PTKCampaignManager sharedManager];
   [cm createInvoiceWithCampaign:campaign donationInvoiceDetails:donationInvoiceDetails completion:^(PTKDonationInvoice *invoice, NSError *error) {
        if (invoice) {
            PTKMoney *amountToBeDonated = invoice.amount;
        }
    }];</pre>

<br />

# Paying for a Donation Invoice

Once you have created an invoice for an appeal you can [Pay]({{site.baseurl}}/tag-mobile-sdks/0.9.8/ios/payments/) the invoice.

# Gift Aid

If the user is a UK taxpayer, has a UK address and confirms they are eligible for Gift Aid (e.g. through a checkbox) then you can provide the address when creating the invoice to allow registered charities to reclaim the tax on the donation.

# Repeated Donations

You can schedule a donation to be repeated every month when creating the invoice by setting `repeated = YES`.