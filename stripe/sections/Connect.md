# Connect
 
> A **clear and concise revision summary** for the **"Connect" section** of the Stripe documentation, focused on the **Stripe Associate Architect Certification** exam.

---

## 🔗 **Stripe Connect — 15% of Exam Weight**

Stripe Connect is for platforms and marketplaces that manage payments on behalf of others (e.g. Uber, Shopify).

---

### ✅ **1. Connect Features, Account Types, Funds Flow, Onboarding & Reporting**

#### 🌐 **Connect Account Types:**

| Type         | Control               | Stripe Dashboard | KYC                          | Use Case                 |
| ------------ | --------------------- | ---------------- | ---------------------------- | ------------------------ |
| **Standard** | User                  | Yes              | Handled by Stripe            | Simple SaaS              |
| **Express**  | Partial (Stripe UI)   | Yes (limited)    | Handled by Stripe            | Marketplaces             |
| **Custom**   | Full platform control | No               | Platform handles KYC via API | Full white-label control |

#### 💸 **Funds Flow Options:**

* **Destination Charges** (platform controls charge and sends payout to connected account).
* **Separate Charges and Transfers** (charge on one account, transfer funds to another).
* **Direct Charges** (connected account is the merchant of record; platform charges via their account).

#### 📊 **Reporting Tools:**

* `balance_transactions`, `payouts`, `charges`, `transfers`
* Use `Connect Onboarding` and `Account Links API` for Express/Custom user onboarding
* Stripe provides **dashboard visibility**, and **transaction-level reconciliation**

---

### ✅ **2. Creating Separate Charges & Transfers**

* **Charge** the customer on the platform account.
* Then **transfer** funds to connected account using `transfer_data`:

```js
stripe.paymentIntents.create({
  amount: 1000,
  currency: 'usd',
  payment_method: 'pm_card_visa',
  confirm: true,
  transfer_data: {
    destination: '{{CONNECTED_ACCOUNT_ID}}',
  },
});
```

---

### ✅ **3. Using Connect with Express Accounts**

* Stripe-hosted onboarding (simple, pre-built UI)
* Stripe handles **KYC, TOS, tax forms**, etc.
* Platform can still control payout schedules and branding
* Use `account_links.create()` to generate onboarding link

---

### ✅ **4. Managing Payout Schedule**

* Custom or Express accounts can have **manual or scheduled payouts**
* Use:

  ```js
  stripe.accounts.update('acct_xxx', {
    settings: {
      payouts: {
        schedule: {
          interval: 'daily' | 'weekly' | 'monthly',
        },
      },
    },
  });
  ```
* Standard accounts manage their own payouts via dashboard

---

### ✅ **5. Onboarding & Verification**

* **KYC (Know Your Customer)**: Stripe collects identity info per country rules
* Use `account_links` to guide connected accounts through onboarding
* Monitor account status with:

  * `account.requirements`
  * `account.capabilities`
* Use **webhooks** to track verification events: `account.updated`, `capability.updated`

---

### ✅ **6. Using Connect with Custom Accounts**

* Platform has **full control** over onboarding, dashboard, and UI
* Platform is **responsible for KYC**, reporting, communication, and risk
* Typically used when Stripe needs to be invisible to end user
* More work, more flexibility

---

### ✅ **7. Creating Direct Charges**

* **Direct Charges** = charge is created **on the connected account** itself
* Funds go directly to connected account
* Platform has limited control after creation
* Use when connected account is the actual seller

```js
const stripe = require('stripe')('CONNECTED_ACCOUNT_SECRET_KEY');
stripe.charges.create({
  amount: 2000,
  currency: 'usd',
  source: 'tok_visa',
});
```

---

### ✅ **8. Disputes & Chargebacks**

* Handled differently based on **charge type**:

  * **Direct charge**: connected account handles dispute
  * **Destination/separate**: platform handles
* Webhook: `charge.dispute.created`
* Best Practices:

  * Collect evidence
  * Monitor Stripe Dashboard regularly
  * Use **Radar** rules to reduce fraud

---

### ✅ **9. Destination Charges on Your Platform**

* Platform creates a charge on its own account, then **automatically routes funds** to the connected account.
* Commonly used for **Express** setups.
* Platform pays Stripe fees, bears liability.
* `transfer_data.destination` is used in `PaymentIntent` or `Charge`.

---

## 🧠 **Quick Summary Table**

| Concept        | Key                                                                   |
| -------------- | --------------------------------------------------------------------- |
| Account types  | Standard, Express, Custom                                             |
| Charges        | Direct, Destination, Separate                                         |
| Payout control | Platform (Custom/Express), Self (Standard)                            |
| Onboarding     | Express (Stripe-hosted), Custom (API), Standard (user signs up)       |
| Disputes       | Based on who owns the charge                                          |
| Fund movement  | Charge + Transfer vs Destination Charge                               |
| Risk & KYC     | Platform’s responsibility (Custom), Stripe handles (Express/Standard) |

---
