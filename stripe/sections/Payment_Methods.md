# Payment Methods

> A detailed yet crisp **revision summary** of the **"Payment Methods"** section from Stripe's docs for your **Associate Architect Certification**:

---

## 💳 Payment Methods — 10% of Exam

Stripe supports a **wide range of payment methods** to help businesses meet local preferences, reduce cart abandonment, and improve conversion. This section focuses on **how, when, and why** to use different payment options — especially in **North America** and **Europe**.

---

### 1. 🚀 **Stripe’s Payment Methods Overview**

Stripe provides a **unified integration** for many payment methods via:

* [**Payment Element**](https://stripe.com/docs/payments/payment-element) (UI component)
* [**Payment Intents API**](https://stripe.com/docs/payments/payment-intents)

You **don’t need to integrate each method separately** — you configure availability by region/customer from the dashboard or API.

📌 Key advantages:

* Reduced development effort
* Built-in localization
* Automatic fallbacks and retries

---

### 2. 🌍 **Common Payment Methods (NA & EU)**

| Region            | Popular Methods                                                    |
| ----------------- | ------------------------------------------------------------------ |
| **North America** | Card Payments (Visa, Mastercard, AmEx), ACH, Apple Pay, Google Pay |
| **Europe**        | SEPA Direct Debit, iDEAL, Bancontact, Klarna, Giropay              |

🛒 [See full guide](https://stripe.com/docs/payments/payment-methods/overview) to match methods by:

* Customer country
* Settlement currency
* Transaction speed
* Refund capabilities

---

### 3. 🔗 **Payment Links**

[**Payment Links**](https://stripe.com/docs/payments/payment-links) allow businesses to:

* Accept payments without coding
* Generate a hosted checkout page with a URL
* Accept **cards**, **wallets**, and **local methods**

📦 Use cases:

* Quick sales via email, SMS, social media
* Freelancers, SaaS trials, donations

🧠 Customizable with logo, theme, success/fail redirects, etc.

---

### 4. 🏦 **Bank Transfer Payments**

Stripe supports:

* **SEPA Credit Transfers** (EU)
* **ACH Credit & Debit Transfers** (US)
* **Wire transfers**

📍 Useful for:

* High-value B2B transactions
* Customers without cards

Flow:

1. Customer gets virtual bank details
2. Sends a transfer
3. Stripe reconciles it to the intended invoice/payment intent using reference code

🔐 Stripe offers automatic reconciliation tools and supports fallback if payment isn’t matched immediately.

---

### 5. ⏸️ **Placing a Hold on a Payment Method**

For cards and some wallets, you can **place a hold (authorization)** before capturing:

📘 Example:

* Car rental charges \$1,000 as an **auth**, captures only \$600 later.

Use `capture_method: manual` when creating a `PaymentIntent`:

```json
{
  "amount": 10000,
  "currency": "usd",
  "capture_method": "manual"
}
```

⏳ Stripe supports holding funds for **up to 7 days** (or 30 days for certain businesses).

---

### ✅ Best Practices

| Goal                     | Best Practice                                |
| ------------------------ | -------------------------------------------- |
| Maximize conversion      | Offer local payment methods                  |
| Quick setup              | Use **Payment Element** or **Payment Links** |
| Handle high-value orders | Use **Bank Transfers** or delayed capture    |
| Support mobile/wallets   | Enable Apple Pay, Google Pay                 |
| Avoid fraud              | Combine with 3D Secure + Radar               |

---

## 🧠 Summary Table

| Concept              | Description                                         |
| -------------------- | --------------------------------------------------- |
| Payment Links        | Hosted Stripe checkout page, no-code                |
| Payment Method Guide | Stripe docs for regional method info                |
| Bank Transfers       | Reconciled manually or via Stripe auto tools        |
| Payment Holds        | Authorize now, capture later                        |
| Supported Regions    | Cards, Wallets (global); iDEAL, SEPA (EU); ACH (US) |

---