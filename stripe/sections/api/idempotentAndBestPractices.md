# 🔁 Idempotent Requests & 🔐 API Security Best Practices

Stripe’s API is built with reliability and security in mind. Two critical concepts to ensure safe and consistent integrations are **idempotency** and **secure usage of the API**.

---

## 🔁 4. Idempotent Requests

### 🧠 What is Idempotency?

Idempotency ensures that multiple identical requests have the **same effect as a single request**. This prevents **duplicate charges**, especially in network retries or failures.

### 📌 Use Cases

- Creating charges
- Creating Payment Intents
- Creating Customers, Subscriptions, etc.

---

### 🛠 How to Use Idempotency in Stripe

Stripe uses the `Idempotency-Key` header to handle this.

```http
POST /v1/payment_intents
Idempotency-Key: abcd-1234-5678

{
  "amount": 2000,
  "currency": "usd",
  "payment_method": "pm_card_visa",
  "confirm": true
}
````

* Stripe stores the first request's result.
* If the same key is used again, the **stored result is returned**, not duplicated.

---

### ⚠️ Best Practices

* Generate a **unique key per operation** (e.g., UUID).
* Keep keys **stable during retries**.
* Avoid using the same key for different resources or different users.

---

### 💡 Idempotency Key Tips

| Tip                         | Why it matters                              |
| --------------------------- | ------------------------------------------- |
| Use UUIDs                   | Ensures uniqueness across systems           |
| Store in logs               | Helps trace issues with retries/duplication |
| Use for write requests only | GET requests are inherently idempotent      |
| Timeout after 24 hours      | Stripe removes old keys after 24 hrs        |

---

## 🔐 5. API Security Best Practices

Protecting your Stripe integration and customer data is critical. Here are core security practices for Stripe usage.

---

### 🔑 1. Keep API Keys Secret

| Key Type        | Where to Use           | Never Do                          |
| --------------- | ---------------------- | --------------------------------- |
| `sk_*` (secret) | Backend servers only   | Never expose to frontend / JS     |
| `pk_*` (public) | Frontend / client-side | Never use to create charges, etc. |

---

### 🔒 2. Environment Management

* Use separate **Live** and **Test** API keys.
* Set keys via **secure environment variables**.
* Avoid hardcoding keys in source code.

---

### 🛂 3. Webhook Signature Verification

* Always verify Stripe webhooks using `stripe-signature` header.
* Use your **signing secret** to validate.

```js
stripe.webhooks.constructEvent(req.body, sig, endpointSecret);
```

---

### 📊 4. Least Privilege Access

* Use **restricted API keys** where possible.
* Assign **minimum required permissions** for services or apps.

---

### 🚧 5. Rotate Secrets Periodically

* Create new keys and **gracefully rotate**.
* Revoke old/compromised keys.
* Automate key rotation policies if possible.

---

### 🧪 6. Test Securely

* Use **test cards** for development.
* Simulate failures and edge cases using test modes and the Stripe CLI.
* Log test activity separately from live usage.

---

### 🧠 7. Common Mistakes to Avoid

| Mistake                                   | What to do instead             |
| ----------------------------------------- | ------------------------------ |
| Exposing `sk_*` in browser                | Use only on secure servers     |
| Not verifying webhook signatures          | Always verify signature hash   |
| Reusing idempotency key for different ops | Use unique keys for unique ops |

---

## 🧠 Exam Tip

Expect questions such as:

* Why use idempotency keys during retries?
* What happens if you reuse a key?
* What API key type should be used in frontend/backend?
* How do you verify that a webhook is legitimate?

---

## 📚 Resources

* [Stripe Docs: Idempotent Requests](https://stripe.com/docs/api/idempotent_requests)
* [Stripe Docs: API Keys](https://stripe.com/docs/keys)
* [Stripe Security Best Practices](https://stripe.com/docs/security/guide)
* [Webhooks Signature Verification](https://stripe.com/docs/webhooks/signatures)