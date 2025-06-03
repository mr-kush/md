# 🔐 Stripe API Keys

API keys are the foundation for authenticating and authorizing API requests in Stripe. They determine access levels, environments, and security practices for platforms and applications using Stripe’s APIs.

---

## 🧾 1. Types of Stripe API Keys

Stripe provides two primary types of keys:

| Key Type         | Purpose                        | Example Prefix   |
|------------------|--------------------------------|------------------|
| **Secret Key**   | Full access to Stripe API      | `sk_live_`, `sk_test_` |
| **Publishable Key** | Used on frontend (read-limited) | `pk_live_`, `pk_test_` |

> ⚠️ **Important:** Secret keys must never be exposed in client-side code.

---

## 🧪 2. Environments: Test vs Live

| Mode  | Key Prefix     | Usage                           |
|-------|----------------|----------------------------------|
| Test  | `sk_test_`, `pk_test_` | Safe for development; use Stripe test cards and simulate webhooks |
| Live  | `sk_live_`, `pk_live_` | Real charges, live customer data |

- Switch environments by changing API keys.
- Use **Stripe CLI** or Dashboard to simulate test events.

---

## 🔁 3. Rotating API Keys

API key rotation is essential for maintaining platform security.

### 🛠 How to Rotate:
1. Go to **Developers > API keys** in the Dashboard.
2. **Create a new key**.
3. Deploy new key to your environment.
4. **Revoke old key** after successful validation.

> 🎯 Tip: Rotate secret keys periodically or after a security incident.

---

## 🔍 4. Managing API Keys in Code

Use environment variables to manage keys securely.

### ✅ Node.js Example

```js
// Load from environment
const stripe = require('stripe')(process.env.STRIPE_SECRET_KEY);

// Securely set in .env
// STRIPE_SECRET_KEY=sk_test_abc123
````

Avoid hardcoding keys into your source code or GitHub.

---

## 🔐 5. Secure Handling of Keys

### ✅ Best Practices

* 🔒 Treat `sk_*` like passwords.
* 🔏 Never expose secret keys to client/browser.
* 🔄 Rotate secret keys on schedule.
* 🔐 Use environment-specific keys (test/live).
* 🧪 Limit test keys to sandbox environments only.

---

## 🛡 6. Viewing & Revoking Keys

**Dashboard Path:**
`Developers → API Keys`

### Actions:

* **View current keys**
* **Create restricted keys** (e.g., read-only for a service)
* **Revoke** old or compromised keys

---

## 👁️ 7. Restricted API Keys

Use [restricted API keys](https://stripe.com/docs/keys#restricted-keys) to limit access for microservices or external apps.

| Restriction Options     | Example Use Case         |
| ----------------------- | ------------------------ |
| Read-only on Customers  | Analytics service        |
| No access to Charges    | Internal monitoring      |
| Full access to Webhooks | Secure webhook processor |

---

## 🔗 Resources

* [Stripe Docs: API Keys](https://stripe.com/docs/keys)
* [Managing Keys Securely](https://stripe.com/docs/security/guide#api-keys)
* [Best Practices for API Usage](https://stripe.com/docs/best-practices)
* [Restricted Keys](https://stripe.com/docs/keys#restricted-keys)

---

## 🧠 Exam Tip

Expect questions around:

* Secret vs Publishable keys
* Use of test vs live environments
* Key rotation and security measures
* How to use keys in Connect (`stripeAccount` header)
