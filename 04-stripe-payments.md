# Stripe & Payments Integration

How to set up payments in your Lovable app using the Stripe integration.

Setting up payments in your app can be done using Lovable's Stripe integration. Before implementing Stripe, it's recommended to ensure that all necessary frontend and backend infrastructure is in place.

For example:
- If you are selling individual products, make sure they are properly implemented, that you have a working shopping cart function and checkout page.
- If you are offering subscriptions, ensure that all login functionalities and different subscription tiers are set up and working correctly.

## Requirements

* The project **must** be connected to Supabase. [Learn more about Supabase integration](03-supabase-integration.md)
* You will also need a Stripe account with the corresponding products set up correctly.

## Implementation Steps

When you're ready to proceed, simply ask the AI to add the integration:

**Example prompt**

```
Add Stripe to collect payments, please.
```

You'll then be presented with a list of prerequisites and an option to enter the Stripe API key. You can find this key in your Stripe account dashboard under **Developers → API keys → Secret key**. Submit the key by clicking on the **"Add API key"** button.

The next step is to add the different price IDs for each product. These can be found by navigating to the product in the Stripe product catalog, clicking on the price, and locating the price ID in the top right corner.

**Example prompt**

```
The vase has the price_id:
xxx

The bowl has the price_id:
xxx

The plate has the price_id:
xxx
```

**Please note**
Stripe integration doesn't work in preview. To test the integration, make sure to deploy. You should also make sure to be in test mode in Stripe when trying out the functionality.

When testing payment, card number: 4242 4242 4242 4242, any 3 digits as CVC and any future date will work as a test card.

## How to Set Up Webhooks Correctly

If you are providing a subscription-based model where paying for a subscription should unlock different tiers on your website, an Edge Function and corresponding webhook are necessary to upgrade user tiers after a payment is successfully processed.

The Edge Function that handles the necessary changes to the user account should be set up automatically by the AI.

### Steps to Set Up Webhooks:

#### 1. Get the Endpoint URL

* Retrieve the **endpoint URL** from the Edge Function that you have set up.
* This can be found under the specific Edge Function details in your Supabase dashboard.

#### 2. Add the Endpoint URL in Stripe

* Navigate to **Developers → Webhooks → Create an event destination** in your Stripe dashboard.
* Select events. If unsure which to select, please ask the AI in chat mode for guidance on which event(s) to choose based on your use case.
* Add the endpoint URL that you retrieved from the Edge Function.

#### 3. Get the Webhook Secret

* Once the webhook is created, copy the webhook secret provided by Stripe.

#### 4. Store the Webhook Secret Securely

* Add the webhook secret to Supabase as a secret value **(Supabase → Edge Functions → Manage secrets → Add new secret)**. Ask the AI in chat mode what the secret should be called to work properly with the Edge function.

By following these steps, your Edge Function and corresponding webhook will be properly set up to handle subscription-based upgrades securely and efficiently.

To troubleshoot during testing you can check Stripe and the specific webhook to see error messages. These error messages can be sent to Lovable for debugging.
