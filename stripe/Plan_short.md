# **compressed 2-day crash plan** for the **Stripe Associate Architect Certification**.

---

## ⚡ **2-Day Intense Study Plan**

### 🎯 **GOAL**

Learn enough to confidently pass the exam by focusing on **core concepts**, **architecture reasoning**, and **feature tradeoffs** (not code-heavy implementation).

---

### 🗓️ **DAY 1: Payments, Billing, Connect, APIs**

#### ✅ **1. Payments (20%) – 2.5 hrs**

* [Payment Intents API](https://stripe.com/docs/payments/payment-intents)
* [Stripe Payment Element](https://stripe.com/docs/payments/payment-element)
* [3D Secure & Card Auth](https://stripe.com/docs/payments/3d-secure)
* [Multiple currencies](https://stripe.com/docs/currencies)
* [Receiving payouts](https://stripe.com/docs/payouts)

🧠 **Focus on:**

* Flow: Elements → Intent → Auth → Capture
* Currency handling & account structure implications

---

#### ✅ **2. Billing (10%) – 1 hr**

* [Stripe Billing Overview](https://stripe.com/docs/billing)
* [Recurring models](https://stripe.com/docs/billing/subscriptions/overview)
* [Subscription upgrade/downgrade](https://stripe.com/docs/billing/subscriptions/upgrade-downgrade)
* [Integration Security](https://stripe.com/docs/security)

🧠 **Focus on:**

* Subscriptions, metered billing, invoicing
* When to use Billing vs. manual charges

---

#### ✅ **3. Connect (15%) – 2 hrs**

* [Connect Overview](https://stripe.com/docs/connect/overview)
* [Custom vs Express](https://stripe.com/docs/connect/accounts)
* [Charge types](https://stripe.com/docs/connect/charges-transfers)
* [Onboarding & Payouts](https://stripe.com/docs/connect/identity-verification)

🧠 **Focus on:**

* Platform architecture: SaaS vs. Marketplace
* Express vs. Custom: who controls UX and payout
* Charge types (direct, destination, separate)

---

#### ✅ **4. API Patterns (5%) – 30 min**

* [API Keys](https://stripe.com/docs/keys)
* [Webhooks](https://stripe.com/docs/webhooks)
* [Idempotency](https://stripe.com/docs/api/idempotent_requests)

🧠 **Focus on:**

* Webhooks are essential for async operations
* Use idempotency keys for retries

---

### 🗓️ **DAY 2: Disputes, Fraud, Methods, Reports, Compliance**

#### ✅ **5. Disputes & Refunds (10%) – 1 hr**

* [Declines vs. Disputes](https://stripe.com/docs/declines)
* [Refunds](https://stripe.com/docs/refunds)
* [Best Practices for Fraud](https://stripe.com/docs/radar/rules)

🧠 **Focus on:**

* Reasons for declines (network vs. fraud)
* Dispute workflows and refund logic

---

#### ✅ **6. Radar & Fraud (10%) – 1 hr**

* [Radar Overview](https://stripe.com/docs/radar)
* [Rules for Radar Teams](https://stripe.com/docs/radar/rules)
* [Risk Signals](https://stripe.com/docs/radar/radar-session)

🧠 **Focus on:**

* Fraud detection layers and custom rules

---

#### ✅ **7. Payment Methods (10%) – 1 hr**

* [Payment Method Guide](https://stripe.com/docs/payments/payment-methods)
* [Bank transfers](https://stripe.com/docs/payments/bank-transfers)
* [Payment links](https://stripe.com/docs/payments/payment-links)
* [Placing holds](https://stripe.com/docs/payments/place-a-hold)

🧠 **Focus on:**

* When to use SEPA, ACH, wallets, or links
* Holding funds (e.g. hotels, security deposits)

---

#### ✅ **8. Reports & Reconciliation (5%) – 30 min**

* [Report Types](https://stripe.com/docs/reports)
* [Balance Transaction Types](https://stripe.com/docs/reports/balance-transaction-types)
* [Reconciliation](https://stripe.com/docs/reports/payout-reconciliation)

🧠 **Focus on:**

* How to explain Stripe reports to Finance teams

---

#### ✅ **9. Global Business & Compliance (5%) – 30 min**

* [Currency Conversion](https://stripe.com/docs/currencies/conversions)
* [Multiple Bank Accounts](https://stripe.com/docs/payouts/multiple-bank-accounts)
* [Cross-border payments](https://stripe.com/docs/global)

🧠 **Focus on:**

* FX fees, cross-border impacts, global availability

---

### ✍️ **10. Final Review (2 hrs)**

* Skim [Study Guide](https://www.stripe.training/study-guide-associate-architect-certification/1569115)
* Revisit sections you flagged during reading
* Try Stripe’s interactive docs & dashboard in test mode
* Draft answers to:

  * How to build a marketplace with payouts?
  * What’s the best setup for a global SaaS?
  * How to reduce fraud?

---

## 🧠 Tips for Success

* Think architecturally — “Which Stripe product fits *this* business problem?”
* Don’t stress about implementation code — focus on capabilities and flows.
* Bookmark Stripe Docs — useful even during open-book scenarios.

---
