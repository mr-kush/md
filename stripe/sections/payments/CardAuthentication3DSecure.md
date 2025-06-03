# 🔐 Card Authentication & 3D Secure in Stripe

## ✅ What is Card Authentication?

Card authentication is the process of verifying that a cardholder is legitimate. Stripe handles this automatically as part of the **Payment Intents API** and **Checkout**.

---

# 🛡️ What is 3D Secure (3DS)?

**3D Secure** is a security protocol used to authenticate cardholders during online payments. It's required in certain regions (like Europe, under **PSD2/SCA** regulations).

## Two Types:

* **3D Secure 1**: Older version, often uses redirects.
* **3D Secure 2 (3DS2)**: Newer, supports biometric, frictionless flows, and better user experience.

---

## ⚙️ Stripe’s Support

Stripe uses **3DS dynamically** — only when required by the card issuer or regulation.

> **Key Benefit:** You don’t need to explicitly trigger 3DS most of the time. Stripe does it based on risk and compliance needs.

---

## ✅ Implementation Overview

When creating a `PaymentIntent`, Stripe will handle 3DS as needed:

```ts
const paymentIntent = await stripe.paymentIntents.create({
  amount: 5000,
  currency: 'eur',
  payment_method_types: ['card'],
  confirm: true,
  return_url: 'https://your-website.com/return',
});
```

Stripe may respond with `requires_action`, prompting a **3DS challenge flow**.

---

## 🔁 Client-Side (Stripe.js / Elements)

On the client, handle authentication like this:

```js
const result = await stripe.confirmCardPayment(clientSecret);
if (result.error) {
  // Handle failure
} else if (result.paymentIntent.status === 'succeeded') {
  // Payment complete
}
```

---

## 🌍 SCA (Strong Customer Authentication)

* Enforced in the **EU/EEA** under **PSD2**.
* Requires **two-factor** customer verification (something the user knows, has, or is).
* Stripe manages this seamlessly.

---

## ⚠️ Common Statuses in 3DS Flows

* `requires_payment_method`: Authentication failed or cancelled.
* `requires_action`: 3DS required.
* `succeeded`: Payment successful.

---

## 🔒 Best Practices

* Always use **Payment Intents API** for card payments.
* Use **Stripe Elements** or **Checkout** to minimize compliance effort.
* Make sure to handle `requires_action` on the client side.
