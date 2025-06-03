# 📬 Stripe Webhooks

Webhooks allow Stripe to notify your server when events occur (e.g., payments succeed, customers are created, disputes are initiated). They are essential for real-time backend automation and platform consistency.

---

## 1️⃣ What Are Webhooks?

Webhooks are **HTTP POST callbacks** sent from Stripe to your server when a Stripe event occurs.

### 🧾 Example Events

- `payment_intent.succeeded`
- `invoice.paid`
- `customer.subscription.created`
- `account.updated` (for Connect)
- `charge.dispute.created`

Each event payload contains a JSON object with:

- `id`: Event ID
- `type`: Event type
- `data.object`: Actual resource (e.g., `payment_intent`, `invoice`)
- `livemode`: Indicates test or live

---

## 2️⃣ How to Set Up Webhooks

### 🛠️ Steps:

1. Go to **Developers → Webhooks** in the Dashboard.
2. Click **“+ Add endpoint”**.
3. Enter your webhook endpoint URL (e.g., `https://example.com/webhooks`).
4. Choose the **events to listen to**.
5. Save and use the **signing secret** to verify the events.

### Optional: Use the [Stripe CLI](https://stripe.com/docs/stripe-cli) to test locally

```bash
stripe listen --forward-to localhost:3000/webhook
````

---

## 3️⃣ Example Webhook Payload

```json
{
  "id": "evt_1ABC...",
  "object": "event",
  "api_version": "2024-03-01",
  "created": 1717000000,
  "data": {
    "object": {
      "id": "pi_12345...",
      "object": "payment_intent",
      "amount": 2000,
      ...
    }
  },
  "livemode": false,
  "type": "payment_intent.succeeded"
}
```

---

## 4️⃣ Handling Webhooks (Example in Node.js)

```js
const express = require('express');
const app = express();
const stripe = require('stripe')(process.env.STRIPE_SECRET_KEY);

const endpointSecret = process.env.STRIPE_WEBHOOK_SECRET;

app.post('/webhook', express.raw({ type: 'application/json' }), (req, res) => {
  const sig = req.headers['stripe-signature'];

  let event;

  try {
    event = stripe.webhooks.constructEvent(req.body, sig, endpointSecret);
  } catch (err) {
    console.error('Webhook signature verification failed.', err);
    return res.status(400).send(`Webhook Error: ${err.message}`);
  }

  // Handle event types
  if (event.type === 'payment_intent.succeeded') {
    const paymentIntent = event.data.object;
    console.log(`PaymentIntent for ${paymentIntent.amount} was successful!`);
  }

  res.json({ received: true });
});
```

---

## 5️⃣ Verifying Webhooks

### 🔐 Why verify?

To confirm the event **came from Stripe** and **wasn’t spoofed**.

### ✅ How?

* Use `stripe-signature` header
* Compare using your **Webhook Secret**

> Never trust webhook requests without signature verification.

---

## 6️⃣ Retry & Delivery Behavior

| Scenario                    | Behavior                                                  |
| --------------------------- | --------------------------------------------------------- |
| Your server returns `2xx`   | Stripe marks the event as successful                      |
| Your server returns `>=300` | Stripe retries for up to **3 days** (exponential backoff) |
| No response / timeout       | Retries initiated                                         |

* Events are delivered **at least once**
* Your webhook handler must be **idempotent**

---

## 7️⃣ Stripe CLI for Webhook Testing

```bash
stripe listen --forward-to localhost:3000/webhook
```

Simulate events:

```bash
stripe trigger payment_intent.succeeded
```

---

## 8️⃣ Tips for Platforms (Stripe Connect)

* Use `account.application.deauthorized`, `account.updated`, `capability.updated`
* Handle events with `stripeAccount` context
* Set up **separate webhook endpoints** for each use case if needed

---

## 🧠 Best Practices

* ✅ Always verify event signature
* ✅ Return a `2xx` response as quickly as possible
* ✅ Use idempotent logic in webhook handlers
* ✅ Store and log the raw payload for debugging
* ✅ Handle both test and live environments
* ✅ Use Stripe CLI for safe local development

---

## 📚 Resources

* [Stripe Webhooks Overview](https://stripe.com/docs/webhooks)
* [Secure Webhook Signing](https://stripe.com/docs/webhooks/signatures)
* [Stripe CLI Docs](https://stripe.com/docs/stripe-cli)

---

## 🧠 Exam Tip

Expect questions on:

* Webhook setup and security
* Signature verification
* Retry behavior and failure handling
* Connect-specific webhook types