# 📘 Stripe Connect Account Types

Stripe Connect supports **three types of connected accounts** based on how much control your platform needs over the **user experience, branding, compliance, and payouts**.

These are:

* **Standard**
* **Express**
* **Custom**

Each account type serves different use cases and offers different levels of **control vs. responsibility**.

---

## 🔷 1. Standard Accounts

### 🔑 Overview

* Users **create and own** a full Stripe account.
* Stripe handles **onboarding, dashboard, support, and compliance**.
* Users log into Stripe directly and manage their settings and payouts.

### ✅ Good For

* Platforms that want **minimum compliance responsibility**.
* Use cases where users should have **full control and visibility** into their financial operations.

### 📌 Key Characteristics

| Feature             | Details                  |
| ------------------- | ------------------------ |
| Onboarding          | Stripe-hosted OAuth flow |
| Dashboard Access    | Full Stripe Dashboard    |
| Control by Platform | Minimal                  |
| Branding            | Stripe-branded           |
| Payout Handling     | User-controlled          |
| Compliance Burden   | Handled by Stripe        |

### 🔄 Example Flow

> Platform redirects user to Stripe → User creates/links Stripe account → Platform receives access token → Platform makes API calls on behalf of user using that token.

---

## 🔷 2. Express Accounts

### 🔑 Overview

* Stripe handles most **onboarding, verification, and compliance**, but users don't get full dashboard access.
* Provides a **lightweight dashboard** for tax documents, payouts, and basic info.

### ✅ Good For

* Marketplaces and gig platforms that want **fast, simple onboarding** but don't need full dashboard control.
* Use cases like ride-sharing, tutoring platforms, creator platforms, etc.

### 📌 Key Characteristics

| Feature             | Details                          |
| ------------------- | -------------------------------- |
| Onboarding          | Stripe-hosted onboarding page    |
| Dashboard Access    | Limited “Express Dashboard”      |
| Control by Platform | Moderate                         |
| Branding            | Stripe with some custom branding |
| Payout Handling     | Stripe-managed                   |
| Compliance Burden   | Stripe (mostly)                  |

### 🔄 Example Flow

> Platform initiates onboarding link → Stripe hosts the onboarding form → User verifies info → Account is created and linked → Platform can collect fees, manage payouts, etc.

---

## 🔷 3. Custom Accounts

### 🔑 Overview

* Platform has **complete control** over the user experience.
* Platform is **responsible for onboarding, UI, and compliance**.
* Suitable for **fully embedded financial experiences**.

### ✅ Good For

* SaaS platforms, vertical software, marketplaces with complex or deeply integrated flows.

### 📌 Key Characteristics

| Feature             | Details                                             |
| ------------------- | --------------------------------------------------- |
| Onboarding          | Platform-built UI using Stripe APIs                 |
| Dashboard Access    | ❌ None (unless built by the platform)               |
| Control by Platform | Full                                                |
| Branding            | 100% platform-branded                               |
| Payout Handling     | Platform-controlled                                 |
| Compliance Burden   | Platform responsible (but Stripe verifies identity) |

### 🔄 Example Flow

> Platform builds its own onboarding UI → Calls Stripe API to collect details → Manages payouts, reporting, refunds, etc. → User doesn’t interact with Stripe UI directly.

---

## 📊 Summary Comparison Table

| Feature           | Standard     | Express       | Custom           |
| ----------------- | ------------ | ------------- | ---------------- |
| Stripe Dashboard  | ✅ Full       | ⚠️ Limited    | ❌ None           |
| Onboarding        | Stripe OAuth | Stripe Hosted | Platform-built   |
| Platform Control  | ❌ Low        | ⚠️ Medium     | ✅ Full           |
| Compliance Burden | ❌ Stripe     | ⚠️ Shared     | ✅ Platform       |
| Branding          | Stripe       | Partial       | Fully Custom     |
| Ideal Use Case    | SaaS Tools   | Marketplaces  | Embedded Fintech |

---

## 🛠️ Key APIs and Tools

* `account.create` – Create a Custom/Express account.
* `accountLinks.create` – Generate onboarding link for Express or Custom.
* `oauth.authorize` – Use with Standard accounts.
* `capabilities` – Set required capabilities (transfers, payouts, card payments).
* `account.update` – Modify account data (especially for Custom accounts).
