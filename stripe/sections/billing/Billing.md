# Billing

> A **focused revision summary** for the **“Billing” section** of the **Stripe Associate Architect Certification**, structured to help with quick understanding and recall.

---

## 💳 **Stripe Billing — 10% of Exam Weight**

Stripe Billing simplifies subscription management, invoicing, and recurring revenue workflows.

---

### ✅ **1. Describe Features, When to Use Them & Migration**

**When to Use Stripe Billing:**

* You offer **subscriptions** or **recurring services**.
* You need **automated invoicing** or **one-time billing**.
* You want to **send smart recovery emails** or **automate retries**.

**Core Features:**

* Subscriptions
* Invoices
* Smart retries for failed payments
* Proration & scheduled changes
* Dunning (email reminders)
* Usage-based billing
* Tax & proration handling

**Migrating to Stripe Billing:**

* Migrate plans, prices, and customer records.
* Use `SubscriptionSchedule` for planned changes.
* Migrate usage data if needed.
* Ensure invoice behavior mimics your current system (e.g., due dates, proration).

---

### ✅ **2. Collecting Online Payments**

* Use the **Payment Element** or **Hosted Invoice Page** to collect payments.
* Payment can be:

  * **Upfront (subscription start)**
  * **Post-invoicing** (net terms)
* Integrate with Stripe Checkout or Elements for collecting billing info.

**Key Objects:**

* `Customer`
* `Subscription`
* `Invoice`
* `PaymentMethod`

---

### ✅ **3. Recurring Pricing Models**

Stripe supports:

| Model                     | Example                                            |
| ------------------------- | -------------------------------------------------- |
| **Flat-rate**             | \$10/month                                         |
| **Per-seat**              | \$10/user/month                                    |
| **Usage-based (metered)** | \$0.01 per API call                                |
| **Tiered pricing**        | \$10 for 1–100 units, \$8 for 101–500              |
| **Graduated pricing**     | \$10 for first 100 units, then \$8 per unit beyond |

**Define pricing in `Product` → `Price` objects.**

---

### ✅ **4. Optimizing Authorization Rates**

To **reduce declines** and **increase conversions**:

* Enable **automatic retries** on failed payments.
* Use **Smart Retries** (machine learning-based retry logic).
* Offer **multiple payment methods** (cards, wallets, bank debits).
* Use **Stripe Link** or **Payment Element** for one-click checkout.
* Collect full billing details for better risk scoring.

---

### ✅ **5. Integration Security Guide**

* Use **Client + Server integration**:

  * Client: Collect PaymentMethod via Payment Element.
  * Server: Attach to customer, create Subscription or Invoice.
* Always **authenticate via API keys**, store minimal PII.
* Use **webhooks** to track subscription/invoice lifecycle (`invoice.paid`, `invoice.payment_failed`).
* Apply **idempotency keys** for subscription creation & invoice logic.
* Respect PCI compliance scope via Stripe Elements/Checkout.

---

### ✅ **6. Upgrade & Downgrade Subscriptions**

Handled using:

* **`update subscription`** API.
* Stripe handles **proration** automatically:

  * Calculates unused time credit.
  * Applies charge for new plan tier.
* Can schedule changes via `SubscriptionSchedule`.
* Use `proration_behavior` parameter:

  * `create_prorations`, `none`, `always_invoice`.

Example (change plan):

```js
stripe.subscriptions.update('sub_123', {
  items: [{ id: 'si_456', price: 'price_new' }],
  proration_behavior: 'create_prorations',
});
```

---

### ⚙️ **Key Stripe Billing Objects**

| Object                 | Purpose                       |
| ---------------------- | ----------------------------- |
| `Product`              | Service/item being sold       |
| `Price`                | Billing logic tied to Product |
| `Customer`             | End-user paying               |
| `Subscription`         | Active billing agreement      |
| `Invoice`              | Generated bill                |
| `PaymentIntent`        | Collect payment               |
| `SubscriptionSchedule` | Manage upcoming changes       |

---

### 📌 **Pro Tips for the Exam**

* Understand the full subscription lifecycle: **create → upgrade → fail → retry → cancel**.
* Know how proration and smart retries work.
* Know which API object handles billing change (`Subscription`, `Schedule`, etc.).
* Practice identifying when to use **Subscriptions** vs **Invoices**.

---