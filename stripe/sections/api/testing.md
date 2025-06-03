# 🧪 Stripe Testing Guide

Testing is a critical part of integrating Stripe successfully and securely. Stripe provides tools, cards, and environments to simulate payment flows, error handling, and edge cases — without touching real money.

---

## 🧠 Why Testing Matters

- Prevent production failures
- Simulate all payment outcomes
- Ensure business logic (subscriptions, refunds, disputes) works correctly
- Test fraud prevention & webhook logic

---

## 🧪 Test Mode vs Live Mode

| Feature                | Test Mode                                | Live Mode                     |
|------------------------|-------------------------------------------|-------------------------------|
| Real charges           | ❌ Fake transactions                      | ✅ Real money involved         |
| API Keys               | `sk_test_...`, `pk_test_...`             | `sk_live_...`, `pk_live_...` |
| Dashboard Appearance   | "Viewing test data" banner                | No banner                     |
| Use Cases              | Development, Staging                     | Production only               |

> **Important:** You cannot mix test and live API keys or data.

---

## 💳 Test Cards (No Real Transactions)

Use the following test cards with any future expiration date (`12/34`) and any CVC (`123`).

### ✅ Successful Payments

| Card Type    | Number           | Description            |
|--------------|------------------|------------------------|
| Visa         | `4242 4242 4242 4242` | Always succeeds     |
| Mastercard   | `5555 5555 5555 4444` | Always succeeds     |
| Amex         | `3782 822463 10005`   | 15-digit AMEX       |

---

### ❌ Failed Payments

| Error Simulated       | Card Number           |
|-----------------------|------------------------|
| Card declined         | `4000 0000 0000 0002`  |
| Insufficient funds    | `4000 0000 0000 9995`  |
| Incorrect CVC         | `4000 0000 0000 0127`  |
| Expired card          | `4000 0000 0000 0069`  |

> See the full list: [Test Card Numbers](https://stripe.com/docs/testing#international-cards)

---

## 🛠 Testing with Payment Intents

```bash
stripe trigger payment_intent.succeeded
````

Or simulate via API:

```json
{
  "amount": 2000,
  "currency": "usd",
  "payment_method": "pm_card_visa",
  "confirm": true
}
```

---

## 📡 Testing Webhooks

Use [Stripe CLI](https://stripe.com/docs/stripe-cli):

```bash
stripe listen --forward-to localhost:3000/webhook
```

Trigger events:

```bash
stripe trigger charge.succeeded
stripe trigger invoice.payment_failed
```

---

## 🧾 Other Test Resources

| Resource                 | Test Scenario                              |
| ------------------------ | ------------------------------------------ |
| Test bank accounts       | Simulate ACH / SEPA payments               |
| Test disputes            | Use `pm_card_chargeCustomerFail`           |
| Test fraud (Radar rules) | Custom Radar rule testing                  |
| Test refund logic        | Create a charge → refund via API/Dashboard |
| Test subscriptions       | Use test customers & coupons               |

---

## 🧠 Testing Best Practices

* ✅ Use environment variables for keys (`sk_test_...`)
* ✅ Automate tests for critical flows (e.g., subscriptions, webhooks)
* ✅ Test error scenarios intentionally
* ✅ Validate webhook delivery and retries
* ✅ Simulate 3D Secure flows when needed

---

## 🧠 Exam Tips

Expect questions like:

* Which card simulates a failed payment?
* How do you simulate a webhook?
* Can you use live API keys in test mode?
* How do you test 3D Secure?

---

## 📚 Resources

* [Stripe Docs: Testing](https://stripe.com/docs/testing)
* [Test Cards List](https://stripe.com/docs/testing#international-cards)
* [Stripe CLI](https://stripe.com/docs/stripe-cli)