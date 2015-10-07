---
layout: page
title: Acts on iOS
permalink: /tag-mobile-sdks/ios/acts/
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
	for (ActDataKey actDataKey : act.getActDataKeys()) {
		ActField<?> actField = fieldGenerators.get(actDataKey.getType()).generate(actDataKey);
		actDataFields.put(actDataKey, actField);
		actInformationContainer.addView(actField.getView(), layoutParams);
        }
    }</pre>

# Present the Act Data Fields to the User


# Validate the Data Fields


# Submit the Act Transaction
