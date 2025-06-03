# 🚀 Stripe Connect Onboarding

Stripe offers flexible onboarding options for platforms integrating Connect. These include **Hosted Onboarding for Express accounts**, fully **Custom onboarding flows**, and built-in **identity verification requirements** for compliance.

---

## 🧭 Onboarding Methods Overview

| Onboarding Type     | Who Controls UI      | KYC Managed By | Account Type |
|---------------------|----------------------|----------------|--------------|
| Hosted (Express)    | Stripe               | Stripe         | Express      |
| Custom Flow         | Your platform (you)  | Stripe         | Custom       |

---

## 1️⃣ Hosted Onboarding (Express Accounts)

Stripe hosts the full onboarding flow using a secure, embeddable **Account Link**. This allows you to onboard users quickly without building your own UI or handling KYC.

### 🔹 Features:
- Stripe handles UI, localization, and compliance.
- You generate a **hosted onboarding link**.
- Accounts are of type **Express**.
- Stripe sends emails, handles updates, and dashboard access.

### 🧾 Example: Create Express Account + Account Link
```js
const account = await stripe.accounts.create({
  type: 'express',
});

const accountLink = await stripe.accountLinks.create({
  account: account.id,
  refresh_url: 'https://example.com/reauth',
  return_url: 'https://example.com/return',
  type: 'account_onboarding',
});
````

> 🔗 Redirect the user to `accountLink.url` to complete onboarding.

---

## 2️⃣ Custom Onboarding Flows

You fully control the UI and collect information from the user, then send it to Stripe using the API.

### 🔹 Features:

* Full control of UX, styling, and flow.
* You collect **person, business, and external account** information.
* You must monitor `capabilities` and `requirements` objects.
* Stripe handles compliance under the hood.

### 🔧 Custom Account Creation Example

```js
const account = await stripe.accounts.create({
  type: 'custom',
  country: 'US',
  email: 'user@example.com',
  capabilities: {
    card_payments: { requested: true },
    transfers: { requested: true },
  }
});
```

> ⚠️ You are responsible for collecting **required fields** from `account.requirements`.

---

## 3️⃣ Verification Requirements

Stripe automatically determines which information is required for compliance (e.g., KYC, AML, local laws).

### 🔍 Two Key Objects:

* `capabilities`: The services the account is allowed to use (e.g., `card_payments`, `transfers`)
* `requirements`: What information is still needed (e.g., legal name, tax ID, address)

### 📦 Example: Reading Verification Status

```js
const account = await stripe.accounts.retrieve('acct_123');
console.log(account.requirements.currently_due);
```

> 📘 Use `currently_due`, `eventually_due`, and `past_due` to build onboarding UIs dynamically.

---

## 🧾 Required Information (Example for US Individual)

| Field                        | Required? |
| ---------------------------- | --------- |
| First/Last Name              | ✅ Yes     |
| Date of Birth                | ✅ Yes     |
| Address                      | ✅ Yes     |
| SSN Last 4 Digits            | ✅ Yes     |
| Email / Phone                | ✅ Yes     |
| External Account (Bank/Card) | ✅ Yes     |

> Full list varies by **country**, **business type**, and **capabilities**.

---

## 🧠 Tips for a Smooth Onboarding

* ✅ Use [webhooks](https://stripe.com/docs/webhooks) to track onboarding progress via `account.updated`.
* ✅ Always check `requirements.disabled_reason` if capabilities are paused.
* ✅ If users fail to complete onboarding in time, generate a new Account Link.

---

## 📚 Resources

* [Express Onboarding](https://stripe.com/docs/connect/express-accounts)
* [Custom Accounts Guide](https://stripe.com/docs/connect/custom-accounts)
* [Verification Requirements](https://stripe.com/docs/connect/identity-verification)
