# 📘 Stripe Connect Features Overview

**Stripe Connect** is Stripe’s solution for **platforms and marketplaces** that need to **manage payments on behalf of third-party users** (e.g., sellers, service providers, contractors, etc.).

It lets your platform **route payments**, **take fees**, **manage onboarding**, and **handle payouts** to your users while ensuring regulatory compliance.

---

## ✅ Key Features of Stripe Connect

---

### 1. **Multiple Account Types**

Stripe Connect supports three different types of connected accounts, depending on how much control you want over the user experience:

| Account Type | Managed by | Use Case                                       | Dashboard Access |
| ------------ | ---------- | ---------------------------------------------- | ---------------- |
| **Standard** | Stripe     | User signs up for their own Stripe account     | ✅ Yes            |
| **Express**  | Shared     | Quick onboarding with limited Stripe dashboard | ✅ Limited        |
| **Custom**   | Platform   | Fully controlled by the platform               | ❌ No             |

---

### 2. **Seamless Onboarding**

Stripe provides tools to onboard users via:

* **Hosted onboarding** flows (especially for Express).
* **Custom-built onboarding** using Stripe APIs (for Custom accounts).

It handles **KYC (Know Your Customer)** and **compliance checks** automatically.

---

### 3. **Flexible Funds Flow**

Stripe Connect supports various ways of moving money:

* **Direct Charges**: Payment goes directly to the connected account.
* **Destination Charges**: Platform collects the money, then routes a portion to the connected account.
* **Separate Charges and Transfers**: Charge any source, then transfer funds to any connected account as needed.

> This flexibility is critical when your platform has different business models (e.g., marketplaces, SaaS, gig work platforms).

---

### 4. **Application Fees & Revenue Sharing**

Platforms can charge **application fees** on payments made to connected accounts:

```json
"application_fee_amount": 1000  // take $10 on a $100 charge
```

This allows platforms to monetize transactions seamlessly.

---

### 5. **Payout Management**

Platforms can:

* Configure payout schedules (daily, weekly, manual).
* Block or delay payouts based on verification or business logic.
* Track all payouts via the Stripe Dashboard or APIs.

---

### 6. **Reporting Tools**

Platforms have access to:

* **Balance & transaction logs**
* **Monthly reports for reconciliation**
* **Fine-grained data** for accounting and user statements

---

### 7. **Compliance Built-In**

Stripe handles:

* Tax reporting (e.g., 1099 forms in the U.S.)
* Identity verification (KYC)
* Anti-money laundering (AML) checks
* PCI compliance

> This lets your platform scale globally without building full fintech infrastructure.

---

### 8. **Webhooks for Automation**

Stripe Connect emits **events** like:

* `account.updated`
* `account.payout.created`
* `transfer.paid`

You can automate workflows (e.g., notify users, release features after verification).

---

## 🌍 Who Uses Stripe Connect?

* **Marketplaces**: e.g., Etsy, Fiverr
* **Crowdfunding Platforms**: e.g., Kickstarter
* **Booking Platforms**: e.g., Airbnb, Booking.com
* **SaaS Platforms**: taking a cut of user payments

---

## ✅ Summary

| Feature          | Description                                     |
| ---------------- | ----------------------------------------------- |
| Account Types    | Standard, Express, Custom                       |
| Onboarding       | Hosted or API-driven                            |
| Funds Flow       | Direct, Destination, Separate Charges/Transfers |
| Platform Revenue | Application fees, revenue splits                |
| Compliance       | KYC, AML, PCI handled                           |
| Reporting        | Balance history, payout details                 |
| Automation       | Webhooks, dashboard, and APIs                   |