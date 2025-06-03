# 🔗 Using Connect with Payment Intents & Setup Intents  
## 💰 Handling Application Fees

Stripe Connect allows platforms to process payments **on behalf of connected accounts**, while collecting **fees** and managing setup flows.

---

## 1️⃣ Overview of Payment Intents in Connect

The [Payment Intents API](https://stripe.com/docs/api/payment_intents) is the recommended way to collect payments under Connect.

### 📦 Key Parameters:

- `amount`: Total amount to charge the customer
- `currency`: Currency of the payment
- `payment_method`: Payment method used
- `application_fee_amount`: Fee collected by the platform
- `transfer_data[destination]`: The connected account receiving the funds

### ✅ Example: Direct-to-connected account with platform fee

```js
const paymentIntent = await stripe.paymentIntents.create({
  amount: 2000,
  currency: 'usd',
  payment_method_types: ['card'],
  application_fee_amount: 300,
  transfer_data: {
    destination: 'acct_connected123',
  },
});
````

> This charges the customer \$20.00, sends \$17.00 to the connected account, and the platform keeps \$3.00.

---

## 2️⃣ Setup Intents with Connect

Use Setup Intents to **securely save a customer's payment method** for future use.

### 📦 Example (for future on\_session or off\_session payments)

```js
const setupIntent = await stripe.setupIntents.create({
  payment_method_types: ['card'],
}, {
  stripeAccount: 'acct_connected123',
});
```

* Required when using **Stripe Elements** or **Checkout** with connected accounts.
* Pass the `stripeAccount` header to scope the intent to a connected account.

---

## 3️⃣ Application Fees

Platforms can **collect fees** when making charges **on behalf of connected accounts**.

### 💵 Fee Types:

| Fee Type                  | When Used                                          |
| ------------------------- | -------------------------------------------------- |
| `application_fee_amount`  | With `PaymentIntent` + `transfer_data.destination` |
| `application_fee_percent` | With Subscriptions (`Subscription.create`)         |

### 📌 Key Considerations:

* Fees are automatically transferred to your **platform account**.
* You can **only set fees** if:

  * The connected account is in **Express** or **Custom** mode
  * The charge is using **destination** or **separate charges & transfers**

---

## 4️⃣ Example: Subscription with Application Fee

```js
const subscription = await stripe.subscriptions.create({
  customer: 'cus_abc',
  items: [{ price: 'price_123' }],
  application_fee_percent: 10,
}, {
  stripeAccount: 'acct_connected123',
});
```

> Stripe will collect 10% of each invoice’s total and send it to your platform.

---

## 🛡️ Important Headers: `stripeAccount`

Always include the connected account ID in the `stripeAccount` header when operating on behalf of that account.

```js
const stripe = require('stripe')('sk_test_...');
const setupIntent = await stripe.setupIntents.create(
  { payment_method_types: ['card'] },
  { stripeAccount: 'acct_1A2B3C4D5E' }
);
```

---

## 🧠 Best Practices

* ✅ Use **Payment Intents** for real-time payments with compliance and SCA support
* ✅ Use **Setup Intents** for saving cards with SCA
* ✅ Collect application fees with every charge (if needed)
* ✅ Confirm Payment/Setup Intents **client-side** using Stripe.js
* ✅ Track `payment_intent.succeeded` and `setup_intent.succeeded` webhooks

---

## 📚 Resources

* [Payment Intents and Connect](https://stripe.com/docs/connect/destination-charges#using-the-payment-intents-api)
* [Application Fees](https://stripe.com/docs/connect/collecting-fees)
* [Setup Intents](https://stripe.com/docs/api/setup_intents)
* [Platform Payments Guide](https://stripe.com/docs/connect/charges)