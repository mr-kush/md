# 🧩 Stripe Payment Element – Detailed Guide

## 🔍 What is the Payment Element?

Stripe's **Payment Element** is an embeddable UI component that allows customers to **pay with multiple payment methods** using a single integration. It's part of the **Stripe.js + Elements** library and is the **recommended way to build a modern checkout**.

---

## 🎯 Why Use Payment Element?

| ✅ Benefits                   | 💡 Details                                                                    |
| ---------------------------- | ----------------------------------------------------------------------------- |
| Unified checkout             | Supports cards, wallets, bank debits, bank transfers, Buy Now Pay Later, etc. |
| Automatic localization       | Localized in 30+ languages automatically based on the customer’s browser      |
| Adaptive UX                  | Adjusts layout and method order dynamically                                   |
| Built-in 3D Secure support   | SCA-compliant with minimal setup                                              |
| Payment method expansion     | Add new payment methods from dashboard, no code change needed                 |
| One-time & recurring support | Works for both types of transactions                                          |

---

## 🏗️ Key Components of the Payment Element Flow

1. **Customer selects payment method** from the Payment Element UI.
2. You **create a PaymentIntent** or SetupIntent on the server.
3. Stripe shows the appropriate form.
4. You **confirm the payment** with the Payment Element client-side.
5. You handle webhooks for fulfillment.

---

## ⚙️ Server-side: Create a PaymentIntent

```ts
const paymentIntent = await stripe.paymentIntents.create({
  amount: 2000,
  currency: 'usd',
  automatic_payment_methods: { enabled: true },
});
```

> This enables **automatic discovery of the best payment methods** for the customer.

---

## 🎨 Client-side Integration

```html
<!-- Include Stripe.js -->
<script src="https://js.stripe.com/v3/"></script>
```

```ts
const stripe = Stripe('pk_test_...');
const elements = stripe.elements({ clientSecret });

const paymentElement = elements.create('payment');
paymentElement.mount('#payment-element');
```

### 🔘 Confirm Payment

```ts
const { error } = await stripe.confirmPayment({
  elements,
  confirmParams: {
    return_url: 'https://yourdomain.com/checkout/complete',
  },
});
```

---

## 🧠 Payment Element Internals

| Feature                     | Description                                                           |
| --------------------------- | --------------------------------------------------------------------- |
| `automatic_payment_methods` | Enables Stripe to decide best methods based on region, currency, etc. |
| SetupIntents support        | Use for saving cards or setting up recurring payments                 |
| `return_url`                | Required for redirect-based methods (e.g., iDEAL, Bancontact, SEPA)   |
| Dynamic Updates             | Can be re-mounted if payment method is updated                        |
| Billing details auto-fill   | Use `customer` and `payment_method_data.billing_details` for auto-pop |

---

## 🔐 Payment Method Support Matrix (as of 2024)

| Payment Method    | Region     | Supports Recurring? | Redirect? |
| ----------------- | ---------- | ------------------- | --------- |
| Cards             | Global     | ✅ Yes               | ❌         |
| Apple Pay / GPay  | Global     | ✅                   | ❌         |
| iDEAL             | EU (NL)    | ❌                   | ✅         |
| Bancontact        | EU (BE)    | ❌                   | ✅         |
| EPS               | EU (AT)    | ❌                   | ✅         |
| Klarna            | EU, US     | ✅ (via setup)       | ✅         |
| SEPA Direct Debit | EU         | ✅                   | ❌         |
| US Bank Transfers | US         | ✅                   | ✅         |
| BLIK, Giropay     | Poland, DE | ❌                   | ✅         |

→ Stripe manages this dynamically via **automatic\_payment\_methods**.

---

## 🔁 One-Time vs Recurring Payments

| Flow Type | Intent Type                | Details                                                            |
| --------- | -------------------------- | ------------------------------------------------------------------ |
| One-time  | PaymentIntent              | Use to charge immediately                                          |
| Recurring | SetupIntent + Subscription | Setup payment method, attach to customer, then create subscription |

---

## 👨‍💻 Example Flow: Recurring Payment

1. Create a customer
2. Create SetupIntent
3. Mount Payment Element
4. Confirm setup
5. Attach `payment_method` to subscription

---

## 🔄 Updating Payment Element (Optional)

If you need to update the intent or customer details dynamically (e.g., currency change), you can destroy and reinitialize the element.

```ts
paymentElement.unmount();
elements.update({ clientSecret: NEW_CLIENT_SECRET });
```

---

## 🛡️ 3D Secure & SCA Support

* Automatically handled by Stripe when required
* Stripe will **trigger redirect or modal flow** when needed
* Use `handleCardAction()` only if needed (legacy)

---

## 🪄 Design Customization (CSS)

Stripe allows light customization using:

* `appearance` object
* Custom fonts and colors
* UI themes: `theme: 'stripe' | 'night' | 'flat' | 'none'`

```ts
const elements = stripe.elements({
  clientSecret,
  appearance: {
    theme: 'flat',
    variables: {
      colorPrimary: '#000',
      fontFamily: 'Montserrat',
    },
  },
});
```

---

## 🧾 Testing with Payment Element

Use [Stripe test cards](https://stripe.com/docs/testing) depending on the method:

* Visa: `4242 4242 4242 4242`
* 3DS Card: `4000 0025 0000 3155`
* iDEAL: Any name works, triggers redirect
* Klarna: Works with customer email

---

## 📦 Bundled with Stripe Checkout

If you're using **Stripe Checkout**, it also uses Payment Element internally for automatic PM selection. But with **Elements**, you control UI and logic fully.

---

## 🧠 Pro Tips

* Use `automatic_payment_methods` to scale globally.
* Localize with `locale: 'auto'` or set your own.
* Handle `payment_intent.succeeded` via webhooks for fulfillment.
* Always keep a fallback UI for redirect-based methods.

---

## 🧮 Payment Element vs Other Elements

| Feature          | Payment Element | Card Element | Checkout |
| ---------------- | --------------- | ------------ | -------- |
| All PMs          | ✅               | ❌            | ✅        |
| Hosted UI        | ❌               | ❌            | ✅        |
| Custom UX        | ✅               | ✅            | ❌        |
| Recurring ready  | ✅               | ✅            | ✅        |
| Global readiness | ✅               | ❌            | ✅        |
