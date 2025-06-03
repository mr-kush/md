# 🔁 Stripe Subscriptions: Upgrade & Downgrade Handling

Managing **subscription changes**—whether upgrades, downgrades, or billing cycle adjustments—is a core part of Stripe Billing. This guide covers how to handle these changes using Stripe's APIs and best practices.

---

## 🔧 1. Changing a Subscription

To **change a subscription**, you typically:

- Update the `subscription` object
- Modify the `items` (i.e., the prices/tiers)
- Decide how to handle **proration**

---

### 🟢 1.1 Basic Example: Upgrade to Higher Tier

```bash
POST /v1/subscriptions/sub_123
{
  items[0][id]: si_abc123,
  items[0][price]: price_premium,
  proration_behavior: create_prorations
}
````

This replaces the current plan with a higher-priced plan and calculates a **prorated charge** for the remaining cycle.

---

## ⚖️ 2. Proration Behavior

Stripe automatically handles billing adjustments unless told otherwise.

| Option              | Description                                  |
| ------------------- | -------------------------------------------- |
| `create_prorations` | Default. Applies prorated charges or credits |
| `always_invoice`    | Create invoice immediately                   |
| `none`              | No proration (change is silent)              |

---

### 🔄 2.1 When to Disable Proration

* Silent plan transitions
* End-of-cycle upgrades
* Promotional use cases

```bash
proration_behavior: none
```

---

## 🕒 3. Mid-Cycle Changes

You can change plans immediately or at the end of the current billing period.

* Use `cancel_at_period_end: true` to **defer change**
* Schedule updates with `subscription_schedules`

---

### 🧠 Scheduled Upgrades/Downgrades

```bash
POST /v1/subscription_schedules
{
  customer: cus_123,
  start_date: now,
  end_behavior: release,
  phases: [
    {
      items: [{ price: price_basic }],
      iterations: 1
    },
    {
      items: [{ price: price_premium }]
    }
  ]
}
```

---

## 🔂 4. Quantity Adjustments

In per-seat billing, changing `quantity` = upgrading or downgrading:

```bash
POST /v1/subscription_items/si_123
{
  quantity: 10
}
```

> You can also add/remove items for multi-plan subscriptions.

---

## 🧠 Best Practices

* 💡 **Test proration logic** in test mode with different time windows
* ✅ Confirm invoice amounts via the API or Dashboard before confirming changes
* 📩 Notify customers when their plan or bill amount changes
* 🧾 Use `invoice_now: true` to bill immediately if needed

---

## 🧪 Testing Scenario

* Create a subscription with a basic plan
* After 10 days, upgrade to a premium plan
* Confirm proration appears on the next invoice

---

## 📚 Resources

* [Subscription Changes (Stripe Docs)](https://stripe.com/docs/billing/subscriptions/upgrade-downgrade)
* [Subscription Schedules](https://stripe.com/docs/billing/subscriptions/subscription-schedules)
* [Proration Behavior](https://stripe.com/docs/billing/subscriptions/prorations)