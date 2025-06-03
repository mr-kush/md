# 🌍 Working with Multiple Currencies in Stripe

## ✅ Key Concepts

* Stripe **supports 135+ currencies** globally.
* Charges, payouts, and reporting are all currency-aware.
* **Each charge must specify a currency.**

---

## 💱 Currency Support

You can charge customers in their **local currency** and receive payouts in your **settlement currency** (often based on your bank location).

```ts
const paymentIntent = await stripe.paymentIntents.create({
  amount: 5000,
  currency: 'eur', // Example: 50 EUR
  payment_method_types: ['card'],
});
```

---

## 🔁 Currency Conversion

* Stripe **automatically converts** the charge currency to your **payout currency** using real-time exchange rates.
* A **conversion fee** (typically 1%) is applied on top of Stripe’s standard processing fees.

---

## 🏦 Settlement Currency

* Depends on your **Stripe account country** and **connected bank**.
* You can **add multiple bank accounts** for different currencies to reduce conversion costs.

> Example: If your account is in the US, but you receive a charge in EUR, Stripe converts EUR ➝ USD unless you have an EUR-denominated bank account.

---

## ⚖️ Reporting Considerations

* **Balance transactions** show original and converted amounts.
* Reports include `currency` and `amount` fields.
* Use [Stripe’s balance API](https://docs.stripe.com/api/balance) or the **Dashboard** for breakdowns.

---

## 📌 Tips

* Set currency per product/charge.
* Avoid conversions by using matching currency bank accounts.
* Use `Stripe Checkout` or `Elements` to localize the experience for users.