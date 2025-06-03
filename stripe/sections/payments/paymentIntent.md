# 🧾 Stripe Payment Intents & the Payment Intents API

---

## 🔹 What is a PaymentIntent?

A **`PaymentIntent`** represents a customer's **intent to pay** and tracks the lifecycle of a payment attempt from start to finish.

Stripe introduced the `PaymentIntent` model to support **Strong Customer Authentication (SCA)** and future-proof payments (e.g., handling 3D Secure, multiple payment steps).

---

## 🧠 Why Payment Intents?

* Enables **compliance with regulations** like SCA in Europe (PSD2).
* Allows handling of **authentication, delays, retries, and confirmations**.
* Provides **robust tracking** of payment states: from initiation to success/failure.

---

## 🔁 Typical Lifecycle of a PaymentIntent

1. **Create a PaymentIntent**
2. **Attach a payment method**
3. **Confirm the PaymentIntent**
4. **Handle authentication (if required)**
5. **Capture (if not auto-captured)**
6. **Succeed or fail**

---

## 📦 Example (Card Payment Flow)

### ✅ 1. Create PaymentIntent

```ts
const paymentIntent = await stripe.paymentIntents.create({
  amount: 5000, // in cents (e.g., $50.00)
  currency: 'usd',
  payment_method_types: ['card'],
});
```

---

### 🔗 2. Attach Payment Method (if needed)

Stripe.js or client SDKs handle this step in most frontends:

```js
const result = await stripe.confirmCardPayment(clientSecret, {
  payment_method: {
    card: cardElement,
    billing_details: { name: 'John Doe' }
  }
});
```

---

### 🚦 3. Confirm + Handle 3D Secure (SCA)

* Stripe automatically triggers **3D Secure** if needed.
* You must handle `requires_action` or `requires_confirmation` statuses.

---

## 🧾 Key Properties of a PaymentIntent

| Field                  | Description                                                  |
| ---------------------- | ------------------------------------------------------------ |
| `status`               | Payment state (e.g., `requires_payment_method`, `succeeded`) |
| `amount`, `currency`   | Amount in minor units (e.g., cents)                          |
| `payment_method_types` | Allowed methods (e.g., `card`, `ideal`, etc.)                |
| `client_secret`        | Secret used by frontend to complete the payment              |
| `confirmation_method`  | `automatic` or `manual`                                      |
| `capture_method`       | `automatic` or `manual` capture of funds                     |
| `metadata`             | For tracking (e.g., order ID)                                |

---

## 🧭 PaymentIntent Statuses

| Status                    | Meaning                                 |
| ------------------------- | --------------------------------------- |
| `requires_payment_method` | Payment failed or cancelled             |
| `requires_confirmation`   | Awaiting confirmation by server/client  |
| `requires_action`         | SCA or authentication step needed       |
| `processing`              | Stripe is confirming the payment        |
| `succeeded`               | Payment was successful                  |
| `canceled`                | Payment was canceled by you or customer |

---

## 🪙 Capture Method (Manual vs Auto)

* **Automatic (default):** Stripe **captures** the funds immediately on success.
* **Manual:** You **authorize** first, then capture within 7 days.

```ts
// Manual capture
const intent = await stripe.paymentIntents.create({
  amount: 10000,
  currency: 'usd',
  capture_method: 'manual',
});

// Later:
await stripe.paymentIntents.capture(intent.id);
```

---

## 🔄 Handling Payment Failures

* When a payment fails, you can update the PaymentIntent with a new payment method and retry:

```ts
await stripe.paymentIntents.update(intent.id, {
  payment_method: 'pm_newcard',
});
```

---

## 🔐 Security Notes

* Never expose the `secret_key` to the client.
* Use the **client secret** only on the frontend.
* Use **idempotency keys** to prevent duplicate charges.

---

## 🧰 Related Webhooks

| Event                            | Purpose                        |
| -------------------------------- | ------------------------------ |
| `payment_intent.succeeded`       | Payment completed successfully |
| `payment_intent.payment_failed`  | Payment failed                 |
| `payment_intent.requires_action` | Authentication step triggered  |
| `payment_intent.canceled`        | PaymentIntent was canceled     |

---

## 🧱 Payment Intents vs Charges

| Aspect       | `PaymentIntent`                    | `Charge` (legacy)                |
| ------------ | ---------------------------------- | -------------------------------- |
| Flow Support | Multi-step, modern, supports SCA   | One-step, simpler                |
| Use Cases    | Cards, wallets, international, SCA | Simple, card-only integrations   |
| Recommended? | ✅ Yes – future-proof & flexible    | ❌ No – deprecated for most cases |

---

## ✅ Best Practices

* Always **create PaymentIntents server-side**.
* Set **`automatic_payment_methods: true`** to accept multiple methods easily.
* Use Stripe Elements or Checkout to reduce SCA complexity.
* Watch **webhooks** for real-time status updates.
* Handle `requires_action` to support 3DS or redirects properly.

---

## 🧪 Testing with Payment Intents

Use Stripe test cards:

| Use Case           | Test Card #           | Result       |
| ------------------ | --------------------- | ------------ |
| Successful payment | `4242 4242 4242 4242` | Succeeds     |
| 3D Secure required | `4000 0025 0000 3155` | Triggers 3DS |
| Payment declined   | `4000 0000 0000 0002` | Fails        |