# API Patterns
> A concise yet detailed **revision summary of the "API Patterns" section** of the Stripe documentation tailored for the **Stripe Associate Architect Certification**:

---

## 🧩 Stripe API Patterns — 5% of Exam

This section tests your understanding of Stripe’s **API architecture**, **event-driven design**, **webhooks**, **security**, and **safe request handling** (idempotency).

---

### 🔑 **1. API Keys**

Stripe uses **secret** and **publishable** keys to authenticate API requests.

| Key Type      | Scope                  | Usage                                                             |
| ------------- | ---------------------- | ----------------------------------------------------------------- |
| `sk_test_...` | Secret key (test)      | Used server-side for secure actions (e.g., create charge, refund) |
| `pk_test_...` | Publishable key (test) | Used client-side for Payment Element or Elements                  |
| `sk_live_...` | Secret key (live)      | For production                                                    |
| `pk_live_...` | Publishable key (live) | For production                                                    |

> **Security Tip:** Never expose your secret keys in frontend code.

---

### 📦 **2. Expanding Responses**

By default, Stripe APIs return object IDs for nested data (e.g., `customer`, `payment_method`). Use the **`expand[]`** parameter to include full objects inline.

#### Example:

```http
GET /v1/payment_intents/pi_123?expand[]=customer&expand[]=charges.data.balance_transaction
```

✅ Use this to:

* Reduce number of API calls
* Preload related data for display or processing

---

### 📡 **3. Webhooks**

Webhooks are **event-driven HTTP callbacks** sent by Stripe when something happens (e.g., payment succeeds, dispute created).

#### Key Concepts:

* You define **webhook endpoints** on your server.
* Stripe sends `event` payloads via `POST`.
* Use **`stripe-cli`** to test webhooks locally:

  ```bash
  stripe listen --forward-to localhost:3000/webhooks
  ```

#### Common Events:

* `payment_intent.succeeded`
* `invoice.paid`
* `charge.dispute.created`
* `checkout.session.completed`

#### Secure Your Webhooks:

* Verify the `Stripe-Signature` header using your **webhook secret key**.

---

### ♻️ **4. Idempotent Requests**

Stripe APIs support **idempotency keys** to safely retry requests (especially important in network timeouts).

#### Why it matters:

* Avoid duplicate charges or resource creation
* Prevent unexpected behavior in retries

#### Example (Node):

```js
stripe.charges.create({
  amount: 2000,
  currency: 'usd',
  source: 'tok_visa',
}, {
  idempotencyKey: 'order_12345',
});
```

> Each idempotency key ensures **the exact same result** is returned for retries with the same parameters.

---

## 🧠 Summary Table

| Concept             | Key Points                                                |
| ------------------- | --------------------------------------------------------- |
| API Keys            | `sk_` (server-side), `pk_` (client-side)                  |
| Expanding Responses | Use `expand[]` param to preload nested data               |
| Webhooks            | Event-driven; verify signature; test with `stripe listen` |
| Idempotency         | Retry-safe operations using `idempotencyKey`              |

---