# 💳 Stripe Billing: Collecting Online Payments & Recurring Pricing Models

Stripe Billing helps businesses manage subscriptions, invoices, and recurring revenue with minimal effort and maximum flexibility.

---

## ✅ 1. Collecting Online Payments

Stripe provides **two primary ways** to collect payments for recurring billing:

### 🔗 1.1 Payment Links

- No code required.
- Generate a hosted payment page via the Dashboard or API.
- Useful for fast, one-off subscription launches or campaigns.

```bash
POST /v1/payment_links
````

**Pros:**

* Fast and simple
* Fully hosted and secure
* Great for MVPs or small-scale products

---

### 🧾 1.2 Stripe Checkout (Hosted)

* Pre-built checkout UI to accept recurring payments (e.g., subscriptions).
* Supports coupon codes, tax collection, 3D Secure, etc.

```js
const session = await stripe.checkout.sessions.create({
  mode: 'subscription',
  line_items: [
    { price: 'price_monthly_123', quantity: 1 }
  ],
  success_url: 'https://example.com/success',
  cancel_url: 'https://example.com/cancel',
});
```

**Use Cases:**

* SaaS subscriptions
* Membership signups
* Trials and promotions

---

### 🧑‍💻 1.3 Custom Payment Flows

* Use Stripe Elements or Payment Intents + Subscriptions API
* Gives full control over UX
* Required for complex integrations (e.g., multi-step onboarding)

---

### 🧠 Tips for the Exam

* Know the difference between Payment Links vs Checkout
* Understand when to use custom UI vs hosted flows
* Know how to set up trial periods, coupons, and email receipts

---

## 🔁 2. Recurring Pricing Models

Stripe supports flexible billing models to suit different types of businesses.

### 📦 2.1 Flat Rate

* Fixed amount per billing cycle

```bash
$10/month for unlimited usage
```

---

### 📊 2.2 Per-Seat (Quantity-Based)

* Charges vary based on `quantity`

```bash
$5/user/month, 10 users = $50
```

Use the `quantity` parameter in the `line_items`.

---

### 📈 2.3 Tiered Pricing

* Different unit costs based on usage **range**

```bash
First 100 units: $0.10
Next 900 units: $0.08
```

> Great for usage-based pricing with volume discounts.

---

### ⏱ 2.4 Metered Billing

* Charges based on actual usage **recorded via API**

```bash
POST /v1/subscription_items/{item_id}/usage_records
{
  quantity: 120,
  timestamp: 1717280000,
  action: 'set'
}
```

Stripe calculates billing automatically at the end of the period.

---

### 🛠 2.5 Proration

* Automatically applied when customers **upgrade or downgrade**
* Can be customized or disabled using `proration_behavior`

---

### 🧠 Tips for the Exam

* Know how to configure `price` objects for each model
* Understand usage-based billing and how to submit usage records
* Be familiar with proration logic and mid-cycle changes

---

## 📚 Resources

* [Stripe Docs: Billing](https://stripe.com/docs/billing)
* [Recurring Pricing Models](https://stripe.com/docs/billing/subscriptions/pricing-models)
* [Payment Links](https://stripe.com/docs/payment-links)
* [Checkout for Subscriptions](https://stripe.com/docs/payments/checkout/subscriptions)