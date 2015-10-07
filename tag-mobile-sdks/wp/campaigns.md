---
layout: page
title: Campaigns on Windows Phone
permalink: /tag-mobile-sdks/wp/campaigns/
---

A Campaign is a particular charity or even a specific cause or event that the user can donate to. Donations can be made on a single-time or on a recurring monthly basis. If the merchant (charity) and consumer are both eligible for a tax-reclaim scheme, such as Gift Aid in the UK, this can be offered through the app.

To make a donation for a campaign create an invoice for the donation using the `CampaignManager`, then make a  [Payment]({{site.baseurl}}/tag-mobile-sdks/wp/payments/) for that invoice.

<br />

# Creating an Invoice for a Campaign

Before creating an invoice you need to ensure the users [Profile]({{site.baseurl}}/tag-mobile-sdks/wp/profile/) has all required information for the merchant.

1. Select a PaymentInstrument from the Profile that is accepted by the Merchant:

    <pre>
    List&lt;PaymentInstrument&gt; acceptedPaymentInstruments = Profile.CurrentProfile.GetAcceptedPaymentInstruments(merchant);
    PaymentInstrument paymentInstrument = acceptedPaymentInstruments[0];
    </pre>

2. Create an DonationInvoiceDetails to provide correct amount, payment instrument, gift aid address for crating an donation invoice. You can also specify if the donation repeats every month.

	<pre>DonationInvoiceDetails donationInvoiceDetails = new DonationInvoiceDetails(amount, repeated, paymentInstrument, giftAidAddress);</pre>

3. Use the CampaignManager to create an invoice for the correct amount, you can also specify if the donation repeats every month:

	<pre>CampaignManager cm = CampaignManager.GetInstance();
	DonationInvoice invoice = cm.CreateInvoiceAsync(campaign, donationInvoiceDetails);
	Money amountToBeDonated = invoice.Amount;</pre>

<br />

# Paying for a Donation Invoice

Once you have created an invoice for a campaign donation you can make a [Payment]({{site.baseurl}}/tag-mobile-sdks/android/payments/) for that invoice.

# Gift Aid

If the user is a UK taxpayer, has a UK address and confirms they are eligible for Gift Aid (e.g. through a checkbox) then you can provide the address when creating the invoice to allow registered charities to reclaim the tax on the donation.

# Repeated Donations

You can schedule a donation to be repeated every month when creating the invoice by setting `repeated = true`.
