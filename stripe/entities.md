# Entities

Stripe uses various **entities** (or "objects") throughout its API and documentation to represent different components of the payment ecosystem. These entities are typically **JSON-based** data structures and are central to understanding how Stripe works.

> Here’s a breakdown of the **most important Stripe entities**, their purpose, and simple examples:

---

## 🔹 1. `Customer`

Represents a customer in your Stripe account. Can store payment methods, billing info, and subscriptions.

### 🧾 Example:

```json
{
  "id": "cus_123abc",
  "email": "jane@example.com",
  "name": "Jane Doe",
  "payment_methods": ["pm_1", "pm_2"]
}
```

---

## 🔹 2. `PaymentIntent`

Represents the lifecycle of a payment (especially for card-based and SCA-compliant payments).

### 🧾 Example:

```json
{
  "id": "pi_1A2b3C4d5E",
  "amount": 2000,
  "currency": "usd",
  "status": "succeeded",
  "customer": "cus_123abc"
}
```

---

## 🔹 3. `SetupIntent`

Used to save a payment method for future use (without charging immediately).

### 🧾 Example:

```json
{
  "id": "seti_123",
  "status": "succeeded",
  "payment_method": "pm_card_visa"
}
```

---

## 🔹 4. `Subscription`

Manages recurring billing for customers using Stripe Billing.

### 🧾 Example:

```json
{
  "id": "sub_456",
  "customer": "cus_123abc",
  "items": [{ "price": "price_789" }],
  "status": "active"
}
```

---

## 🔹 5. `Invoice`

Represents a statement of amounts owed by a customer; generated for subscriptions or manual billing.

### 🧾 Example:

```json
{
  "id": "in_123",
  "amount_due": 1000,
  "status": "open",
  "customer": "cus_123abc"
}
```

---

## 🔹 6. `Charge`

Represents a single attempt to move money from a customer’s payment method.

> ⚠️ Stripe recommends using `PaymentIntent` instead for newer integrations.

### 🧾 Example:

```json
{
  "id": "ch_123",
  "amount": 1000,
  "currency": "usd",
  "status": "succeeded"
}
```

---

## 🔹 7. `Payout`

Used to send funds from Stripe to a connected account’s external bank.

### 🧾 Example:

```json
{
  "id": "po_123",
  "amount": 5000,
  "currency": "usd",
  "destination": "ba_456"
}
```

---

## 🔹 8. `BalanceTransaction`

Describes any transaction that affects the Stripe balance (charges, payouts, refunds, etc.)

### 🧾 Example:

```json
{
  "id": "txn_789",
  "amount": 1000,
  "type": "charge",
  "net": 970,
  "fee": 30
}
```

---

## 🔹 9. `Product` & `Price`

* **Product**: An item or service you're selling.
* **Price**: Defines the cost and billing frequency.

### 🧾 Example:

```json
{
  "id": "prod_123",
  "name": "Pro Membership"
}
```

```json
{
  "id": "price_abc",
  "product": "prod_123",
  "unit_amount": 1000,
  "recurring": { "interval": "month" }
}
```

---

## 🔹 10. `Account`

Used for Stripe Connect — represents a connected seller or platform account.

### 🧾 Example:

```json
{
  "id": "acct_1ABC",
  "type": "custom",
  "email": "seller@example.com"
}
```

---

## 🔹 11. `WebhookEvent`

Represents an event sent by Stripe to your backend (e.g., `payment_intent.succeeded`).

### 🧾 Example:

```json
{
  "id": "evt_1XYZ",
  "type": "invoice.payment_succeeded",
  "data": {
    "object": { "id": "in_123", "status": "paid" }
  }
}
```

---

## ⚙️ Other Notable Stripe Entities

| **Entity**            | **Description**                                                                   | **Basic Example**                                                  |
| --------------------- | --------------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| `Refund`              | Represents the refund of a charge or partial refund.                              | `{ "id": "re_123", "amount": 500, "status": "succeeded" }`         |
| `Dispute`             | Represents a chargeback or dispute raised by the cardholder.                      | `{ "id": "dp_123", "status": "needs_response" }`                   |
| `PaymentMethod`       | Represents a customer’s card, bank account, or digital wallet.                    | `{ "id": "pm_visa", "type": "card", "card": { "brand": "visa" } }` |
| `SetupAttempt`        | Tracks attempts to set up a `PaymentMethod` via a `SetupIntent`.                  | `{ "id": "setatt_123", "status": "succeeded" }`                    |
| `Mandate`             | Authorization to debit a customer (used in ACH, SEPA, etc.).                      | `{ "id": "mandate_abc", "status": "active" }`                      |
| `Transfer`            | Moves funds between Stripe accounts (mainly in Connect platforms).                | `{ "id": "tr_123", "amount": 1000, "destination": "acct_456" }`    |
| `Top-up`              | Adds funds to your Stripe balance manually (for manual payouts or testing).       | `{ "id": "tu_123", "amount": 2000 }`                               |
| `ExternalAccount`     | Represents a bank account or debit card for payouts.                              | `{ "id": "ba_123", "object": "bank_account" }`                     |
| `LoginLink`           | Single-use link for a connected account to log into their Stripe Dashboard.       | `{ "url": "https://connect.stripe.com/login_links/abc" }`          |
| `Balance`             | Represents the total and available Stripe balance across currencies.              | `{ "available": [{ "currency": "usd", "amount": 50000 }] }`        |
| `BalanceTransaction`  | Any event that changes your Stripe balance (charges, refunds, fees, payouts).     | `{ "id": "txn_123", "type": "charge", "fee": 300 }`                |
| `Application Fee`     | Fee collected by a platform using Stripe Connect.                                 | `{ "id": "fee_123", "amount": 100, "application": "ca_456" }`      |
| `FeeRefund`           | Refund of an application fee.                                                     | `{ "id": "fr_123", "amount": 100 }`                                |
| `VerificationSession` | Used with Stripe Identity to verify identity documents and selfies.               | `{ "id": "vs_123", "status": "verified" }`                         |
| `TaxRate`             | Defines tax percentage rates (e.g. 7.5%) for invoices/subscriptions.              | `{ "id": "txr_123", "percentage": 7.5 }`                           |
| `TaxId`               | Represents a customer’s tax ID (VAT, GST, etc.).                                  | `{ "id": "txi_123", "type": "eu_vat" }`                            |
| `CountrySpec`         | Lists available payment methods, regulations, and requirements per country.       | `{ "id": "country_spec", "country": "DE" }`                        |
| `File`                | Represents files uploaded to Stripe (e.g., identity docs, receipts).              | `{ "id": "file_abc", "purpose": "dispute_evidence" }`              |
| `FileLink`            | Secure link to access a `File` entity.                                            | `{ "url": "https://files.stripe.com/xyz" }`                        |
| `Event`               | Webhook event from Stripe (e.g., `invoice.paid`, `charge.refunded`).              | `{ "id": "evt_123", "type": "charge.succeeded" }`                  |
| `AccountLink`         | Used in onboarding flows to redirect connected accounts.                          | `{ "url": "https://connect.stripe.com/setup/s/xyz" }`              |
| `Capability`          | Represents features enabled or required on a Connect account (e.g., transfers).   | `{ "id": "transfers", "requested": true }`                         |
| `WebhookEndpoint`     | Represents your server’s endpoint configuration to receive Stripe webhook events. | `{ "id": "we_123", "url": "https://example.com/webhooks" }`        |

---

## 🧠 Tips for Studying These Entities

* Think of entities as **API building blocks** — most API calls return or expect one of these objects.
* Stripe’s **API reference** lists each entity with parameters, responses, and links between them.
* Use Stripe’s [API Explorer](https://stripe.com/docs/api) to see live examples.
  
