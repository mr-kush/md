# Charge

> A **detailed, developer-friendly breakdown of `Charge` objects** in Stripe, especially relevant for your **Stripe Associate Architect Certification**.

---

## 📦 Stripe Charge Object – Deep Dive

The `Charge` object is a **core concept** in Stripe's **Payments API**, representing the **movement of funds from a customer to a Stripe account**. In essence, when a payment is successful, it results in a `charge`.

> 🔗 Stripe Docs Reference: [`/docs/connect/charges`](https://docs.stripe.com/connect/charges)

---

## 🧠 When is a `charge` created?

* Automatically by Stripe when you confirm a [`PaymentIntent`](https://stripe.com/docs/api/payment_intents)
* Or manually (legacy) using the [Charges API](https://stripe.com/docs/payments/charges) (not recommended for new implementations)

---

## ⚙️ Charge Object Structure

A `charge` object is returned as part of the response from payment confirmation.

```json
{
  "id": "ch_1NpTQm2eZvKYlo2C9l1F3GJh",
  "amount": 2000,
  "currency": "usd",
  "status": "succeeded",
  "captured": true,
  "paid": true,
  "payment_method_details": {...},
  "receipt_url": "https://pay.stripe.com/receipts/acct_...",
  ...
}
```

| Key Field                | Description                                                 |
| ------------------------ | ----------------------------------------------------------- |
| `id`                     | Unique identifier for the charge                            |
| `amount`                 | Amount charged in **smallest currency unit**                |
| `currency`               | Currency used                                               |
| `status`                 | `succeeded`, `pending`, `failed`                            |
| `paid`                   | Boolean flag showing whether charge was successful          |
| `captured`               | Whether the charge was captured (useful for authorizations) |
| `payment_method_details` | Card, bank, or other payment method metadata                |
| `transfer_data`          | Relevant when used with Connect (platform payouts)          |

---

## 🧾 Creating a Charge (Legacy — not recommended)

```bash
curl https://api.stripe.com/v1/charges \
  -u sk_test_...: \
  -d amount=2000 \
  -d currency=usd \
  -d source=tok_visa \
  -d description="One-time payment"
```

Stripe now recommends creating a **PaymentIntent**, which automatically creates a `charge` upon confirmation.

---

## 💳 Capture vs Authorize

You can **authorize a payment** and **capture it later**:

```ts
// Authorize only
await stripe.paymentIntents.create({
  amount: 1000,
  currency: 'usd',
  capture_method: 'manual',
  ...
});
```

Later:

```ts
await stripe.paymentIntents.capture('pi_...');
```

---

## 🤝 Connect Platforms and Charges

In Connect, how you create a `charge` affects **fund flows**.

### 1. ✅ Direct Charges (on behalf of connected account)

```ts
stripe.charges.create({
  amount: 1000,
  currency: "usd",
  source: "tok_visa"
}, {
  stripeAccount: '{{CONNECTED_STRIPE_ACCOUNT_ID}}'
});
```

* Charge is made **by the connected account**
* Fees and risk sit with the connected account
* Platform only facilitates

### 2. 🔄 Destination Charges

Platform controls the charge, but **sends funds to the connected account**:

```ts
stripe.charges.create({
  amount: 1000,
  currency: "usd",
  source: "tok_visa",
  destination: {
    account: '{{CONNECTED_STRIPE_ACCOUNT_ID}}'
  }
});
```

* Platform owns the relationship
* Fees and dispute liability often sit with **platform**

### 3. 💸 Separate Charges & Transfers

Split logic into two steps:

* First: charge on platform account
* Then: use `transfer` API to move funds to connected account

```ts
const charge = await stripe.charges.create({
  amount: 1000,
  currency: 'usd',
  source: 'tok_visa',
});

const transfer = await stripe.transfers.create({
  amount: 800,
  currency: 'usd',
  destination: '{{CONNECTED_STRIPE_ACCOUNT_ID}}',
});
```

Useful for marketplaces that retain a **platform fee**.

---

## 🪪 Metadata & Application Fee

Useful metadata and application fee inclusion:

```ts
stripe.paymentIntents.create({
  amount: 2000,
  currency: "usd",
  application_fee_amount: 300,
  transfer_data: {
    destination: "{{CONNECTED_STRIPE_ACCOUNT_ID}}"
  },
  metadata: {
    order_id: "123456"
  }
});
```

---

## 📉 Refunds & Disputes on Charges

* `charge.id` is needed to create a refund
* Refund can be full or partial
* If a dispute arises, Stripe flags it via a **webhook** on the `charge.dispute.created` event

---

## 📊 Reporting Charges

Each `charge`:

* Shows up in **Dashboard**
* Is included in `balance_transactions`
* Is linked to a `payment_intent` (if used)

---

## ✅ Summary Table

| Scenario                   | Charge Method  | Platform Fee?                      | Risk Owner        |
| -------------------------- | -------------- | ---------------------------------- | ----------------- |
| Direct Charge              | Connected acct | No                                 | Connected account |
| Destination Charge         | Platform       | Yes (via `application_fee_amount`) | Platform          |
| Separate Charge & Transfer | Platform       | Yes                                | Platform          |

---

## 📘 Best Practices

* **Always use `PaymentIntent` for new charges**
* Add **metadata** for traceability (order IDs, user IDs, etc.)
* **Capture later** if you're unsure about inventory fulfillment
* Use **Radar + 3DS** for fraud protection

---
