# 👨🏻‍🎓 Stripe Associate Architect Exam

> *Topic-wise MCQs and T/F — with answers included*

## Table of Contents

- [✅ Payments Section (20%)](#-payments-section)
- [✅ Billing Section (10%)](#-billing-section)
- [✅ Connect (15%)](#-connect)
- [✅ API Patterns (5%)](#-api-patterns)
- [✅ Declines, Disputes & Refunds (10%)](#-declines-disputes--refunds)
- [✅ Reporting & Reconciliation](#-reporting--reconciliation)
- [✅ Global Business & Compliance](#-global-business--compliance)
- [✅ Payment Methods](#-payment-methods)
- [✅ Using Radar & Reducing Fraud](#-using-radar--reducing-fraud)

## ✅ Payments Section

**20% of exam** |
Analyze business requirements and propose the best Stripe account structures.

### 🔷 1. Analyzing Business Requirements & Account Structures

#### Q1. A subscription SaaS platform serving customers in multiple countries wants fast onboarding, no responsibility for chargebacks, and easy tax handling. Which Stripe account type is most appropriate?

A) Custom
B) Express
C) Standard
D) Direct Connect

✅ **Answer:** C) Standard

---

#### Q2. A marketplace platform wants full control over payout timing and user experience. Which account type best suits this?

A) Express
B) Standard
C) Custom
D) Connected Standard

✅ **Answer:** C) Custom

---

#### Q3. What Stripe feature allows platforms to separate charge and payout logic?

A) Payment Links
B) Destination Charges
C) Separate Charges and Transfers
D) Direct Charges

✅ **Answer:** C) Separate Charges and Transfers

---

### 🔷 2. Create a Charge

#### Q4. Which of the following APIs is deprecated for direct card payments?

A) Payment Intents
B) Charges API
C) Setup Intents
D) Checkout Sessions

✅ **Answer:** B) Charges API

---

#### Q5. Which API enables SCA compliance, delayed capture, and 3D Secure?

A) Checkout
B) Setup Intents
C) Payment Intents
D) Source API

✅ **Answer:** C) Payment Intents

---

#### Q6. You want to authorize a charge now but capture the funds 3 days later. What is the correct Payment Intents flow?

A) `capture_method: "manual"`
B) `confirmation_method: "automatic"`
C) `capture: false`
D) Use Checkout with `auto_capture: false`

✅ **Answer:** A) `capture_method: "manual"`

---

### 🔷 3. Stripe Payment Element

#### Q7. What is the Stripe Payment Element used for?

A) Creating custom invoices
B) Collecting payment method details in a unified UI
C) Issuing refunds
D) Storing card details

✅ **Answer:** B) Collecting payment method details in a unified UI

---

#### Q8. True or False: The Payment Element requires you to create a Payment Intent before rendering the UI

✅ **Answer:** True

---

#### Q9. What feature allows Stripe to automatically detect and offer local payment methods in the Payment Element?

A) `smart_payment_methods: true`
B) `local_methods: auto`
C) `automatic_payment_methods[enabled]: true`
D) `enable_locale_options: true`

✅ **Answer:** C) `automatic_payment_methods[enabled]: true`

---

### 🔷 4. Receiving Payouts

#### Q10. What determines the frequency of payouts from Stripe to a user’s bank account?

A) Payment method used
B) Account type and payout schedule
C) Customer country
D) Currency selection

✅ **Answer:** B) Account type and payout schedule

---

#### Q11. Which type of Connect account gives the platform full control over payout timing?

A) Express
B) Standard
C) Custom
D) Direct

✅ **Answer:** C) Custom

---

#### Q12. True or False: Stripe always automatically pays out funds to connected accounts as soon as they're available

✅ **Answer:** False (depends on schedule and account type)

---

### 🔷 5. Payment Intents API

#### Q13. What object must be created before using the Payment Element?

A) Payment Method
B) Customer
C) Payment Intent
D) Setup Intent

✅ **Answer:** C) Payment Intent

---

#### Q14. What is the purpose of `client_secret` in the Payment Intents API?

A) It’s used to refund payments.
B) It allows the client-side to complete the payment.
C) It is used for webhook security.
D) It defines the capture method.

✅ **Answer:** B) It allows the client-side to complete the payment.

---

#### Q15. What is the recommended way to retry failed payments requiring authentication?

A) Create a new payment method
B) Restart the checkout session
C) Update the Payment Intent with a new payment method and confirm
D) Use the Refund API and start again

✅ **Answer:** C) Update the Payment Intent with a new payment method and confirm

---

#### Q16. Which of the following is NOT a valid status of a PaymentIntent?

A) `requires_payment_method`
B) `pending_authentication`
C) `requires_action`
D) `succeeded`

✅ **Answer:** B) `pending_authentication` (not a valid status)

---

### 🔷 6. Card Authentication and 3D Secure

#### Q17. What regulation drives the need for 3D Secure in European card payments?

A) PCI-DSS
B) SEPA
C) PSD2
D) GDPR

✅ **Answer:** C) PSD2

---

#### Q18. How does Stripe handle 3D Secure with the Payment Intents API?

A) It prompts merchants to manually request 3DS
B) It detects when 3DS is needed and surfaces `requires_action` status
C) It never uses 3DS for saved cards
D) It handles 3DS automatically on server-side only

✅ **Answer:** B) It detects when 3DS is needed and surfaces `requires_action` status

---

#### Q19. True or False: SCA always requires 3D Secure authentication

✅ **Answer:** False (SCA = Strong Customer Authentication, 3DS is just one method)

---

#### Q20. What parameter do you check to know if customer authentication is needed?

A) `status: “requires_payment_method”`
B) `next_action.type`
C) `error.code`
D) `payment_method.details.auth_required`

✅ **Answer:** B) `next_action.type`

---

### 🔷 7. Working with Multiple Currencies

#### Q21. Which of the following statements about multi-currency support is true?

A) Stripe supports one currency per account
B) You must create a new account for each currency
C) Stripe supports accepting multiple currencies but settles in the default currency
D) Stripe converts currencies only when using Connect

✅ **Answer:** C) Stripe supports accepting multiple currencies but settles in the default currency

---

#### Q22. True or False: You can have separate bank accounts per supported currency in your Stripe dashboard

✅ **Answer:** True

---

#### Q23. Which of the following payment methods supports currency conversion by default?

A) Apple Pay
B) ACH
C) SEPA
D) Card Payments (Visa/Mastercard)

✅ **Answer:** D) Card Payments (Visa/Mastercard)

---

#### Q24. What happens if you accept a currency not supported by your connected bank account?

A) Stripe rejects the payment
B) The payout is paused
C) Stripe automatically converts the funds to your default settlement currency
D) You must create a new account for that currency

✅ **Answer:** C) Stripe automatically converts the funds to your default settlement currency

---

### 🔚 Summary Questions

#### Q25. Which feature ensures payments are processed with regulatory compliance (e.g., PSD2)?

✅ **Answer:** Payment Intents API

---

#### Q26. What do `status: "requires_action"` and `next_action` indicate in a PaymentIntent?

✅ **Answer:** User authentication (e.g., 3D Secure) is required

---

#### Q27. What's the correct order of operations for client-side card collection using the Payment Element?

✅ **Answer:**

1. Create PaymentIntent
2. Load Payment Element
3. Confirm PaymentIntent client-side
4. Handle result

---

#### Q28. You want to accept payments in INR and USD. What do you need?

✅ **Answer:** Add INR and USD support in your account settings, and optionally connect bank accounts for each

---

#### Q29. Which API object allows you to hold a charge and capture it later?

✅ **Answer:** PaymentIntent with `capture_method: manual`

---

#### Q30. What’s a key benefit of using Payment Element vs. custom fields?

✅ **Answer:** Automatically supports multiple payment methods, updated UI, and compliance with local rules

---

## ✅ Billing Section

**10% of exam** |
Describe features, when to use them, and how to migrate to Stripe Billing.

### 🔷 1. Stripe Billing Features & Migration

#### Q1. What is a key benefit of using **Stripe Billing** instead of manually charging users via the Payment Intents API?

A) Allows one-time payments without customer object
B) Manages subscription lifecycles, invoicing, and retries
C) Enables ACH payments only
D) Works only with Connect accounts

✅ **Answer:** B) Manages subscription lifecycles, invoicing, and retries

---

#### Q2. When migrating an existing subscription system to Stripe Billing, what is recommended for **migrating active subscriptions**?

A) Cancel all current subscriptions and create new ones
B) Create one-time invoices for every existing user
C) Use the `subscription_schedule` object and backdate the start date
D) Create `Subscription` objects with a custom billing cycle anchor

✅ **Answer:** D) Create `Subscription` objects with a custom billing cycle anchor

---

#### Q3. True or False: Stripe Billing can be used for both one-time and recurring payments

✅ **Answer:** True

---

#### Q4. What object in Stripe defines how a subscription is billed, including frequency and pricing?

A) Invoice
B) Charge
C) Subscription Item
D) Price

✅ **Answer:** D) Price

---

### 🔷 2. Collecting Online Payments

#### Q5. Which **Stripe-hosted** solution allows you to create a no-code payment flow for recurring billing?

A) Payment Link
B) Payment Element
C) Checkout
D) Terminal

✅ **Answer:** C) Checkout

---

#### Q6. What must be created before collecting a recurring payment with Stripe Billing?

A) Charge
B) Price
C) Subscription
D) Invoice

✅ **Answer:** C) Subscription

---

#### Q7. True or False: Stripe Checkout supports saving a card for future billing in subscription mode

✅ **Answer:** True

---

### 🔷 3. Recurring Pricing Models

#### Q8. What pricing model would be best for a **SaaS company with monthly tiers and optional add-ons**?

A) Flat rate pricing
B) Metered billing
C) Tiered pricing
D) Recurring pricing with multiple Price objects per subscription

✅ **Answer:** D) Recurring pricing with multiple Price objects per subscription

---

#### Q9. You want to bill a customer based on **API usage** each month. What Stripe feature enables this?

A) SetupIntent
B) Metered billing with usage records
C) Tiered pricing
D) Manual invoices

✅ **Answer:** B) Metered billing with usage records

---

#### Q10. True or False: A single Stripe subscription can have multiple pricing components using different billing intervals

✅ **Answer:** False (must share same interval for one subscription)

---

### 🔷 4. Optimizing Authorization Rates

#### Q11. Which Stripe feature **improves recurring authorization success** by retrying intelligently after a decline?

A) Smart Retries
B) Setup Intents
C) Invoice Finalization
D) Manual Charges

✅ **Answer:** A) Smart Retries

---

#### Q12. What setting helps Stripe maximize success of automatic card charges?

A) `payment_behavior: "default_incomplete"`
B) `collection_method: "send_invoice"`
C) Enable **Adaptive Acceptance**
D) Increase retry window to 30 days

✅ **Answer:** C) Enable **Adaptive Acceptance**

---

#### Q13. True or False: Smart Retries are enabled by default in Stripe Billing

✅ **Answer:** True

---

### 🔷 5. Integration Security Guide

#### Q14. What is a key method to **secure your Billing integration**?

A) Use API keys on frontend
B) Use short-lived tokens and secure webhooks
C) Rely only on client-side authentication
D) Skip webhook signature verification in staging

✅ **Answer:** B) Use short-lived tokens and secure webhooks

---

#### Q15. Which Stripe security measure helps verify webhook payloads?

A) HMAC tokens
B) `client_secret` matching
C) `X-Signature` header
D) `Stripe-Signature` header and secret

✅ **Answer:** D) `Stripe-Signature` header and secret

---

#### Q16. True or False: Webhooks are optional when implementing Stripe Billing with recurring payments

✅ **Answer:** False (Webhooks are crucial to track lifecycle events like invoice payment, subscription changes, etc.)

---

### 🔷 6. Upgrade & Downgrade Subscriptions

#### Q17. When a customer downgrades a subscription, what parameter controls whether a **prorated credit** is applied?

A) `payment_behavior`
B) `billing_cycle_anchor`
C) `proration_behavior`
D) `subscription_schedule_mode`

✅ **Answer:** C) `proration_behavior`

---

#### Q18. You want the customer’s plan change to take effect **at the next billing cycle**. What should you set?

A) `billing_cycle_anchor: now`
B) `proration_behavior: none`
C) `subscription_schedule: phase`
D) `effective_date: "next_cycle"`

✅ **Answer:** C) `subscription_schedule: phase`

---

#### Q19. What happens when you **upgrade** a subscription mid-cycle with `proration_behavior: "create_prorations"`?

A) Stripe charges full new plan price
B) Customer is charged only on next cycle
C) Stripe generates prorated charge or credit immediately
D) Subscription is cancelled and restarted

✅ **Answer:** C) Stripe generates prorated charge or credit immediately

---

#### Q20. True or False: You can schedule a future subscription upgrade using the `subscription_schedule` object

✅ **Answer:** True

---

## ✅ Connect

**15% of exam** |
Describe Connect features, account types, funds flow, onboarding, and reporting.

### 🔷 1. Connect Features, Account Types & Funds Flow

#### Q1. Which Stripe Connect account type gives you **maximum control** over onboarding, payments, and payouts?

A) Standard
B) Express
C) Custom
D) Partner

✅ **Answer:** C) Custom

---

#### Q2. What type of account **does NOT give platform access to the dashboard** of the connected account?

A) Express
B) Standard
C) Custom
D) All give dashboard access

✅ **Answer:** C) Custom

---

#### Q3. True or False: Express accounts offer a Stripe-hosted onboarding flow and a Stripe-hosted dashboard

✅ **Answer:** True

---

#### Q4. Which account type uses the **platform’s Stripe keys** to make charges and payouts?

A) Custom
B) Express
C) Standard
D) Partner

✅ **Answer:** A) Custom

---

#### Q5. Which of the following is **true** about Standard accounts?

A) You must implement the onboarding UX
B) Stripe handles KYC and reporting
C) You control payout timing
D) You use your platform’s API keys for payments

✅ **Answer:** B) Stripe handles KYC and reporting

---

### 🔷 2. Creating Separate Charges & Transfers

#### Q6. In a **separate charge and transfer**, the charge is created on

A) The connected account
B) The platform account
C) A third-party account
D) The customer object directly

✅ **Answer:** B) The platform account

---

#### Q7. When using separate charges and transfers, what must you manually specify?

A) `transfer_group`
B) `capture_method`
C) `destination_account`
D) `application_fee`

✅ **Answer:** A) `transfer_group`

---

#### Q8. Which object enables you to **track money movement across multiple Stripe accounts**?

A) `payout`
B) `transfer_group`
C) `payment_link`
D) `session_object`

✅ **Answer:** B) `transfer_group`

---

### 🔷 3. Using Express Accounts

#### Q9. True or False: Express accounts support **destination charges**

✅ **Answer:** True

---

#### Q10. What’s one benefit of Express over Custom?

A) Full control over user experience
B) Stripe handles onboarding and dashboard
C) Full API access to connected account data
D) Supports international cards only

✅ **Answer:** B) Stripe handles onboarding and dashboard

---

#### Q11. You’re building a marketplace that wants **lightweight onboarding and dashboard**, but **controlled payout timing**. Which account type fits?

A) Standard
B) Express
C) Custom
D) Merchant

✅ **Answer:** B) Express

---

### 🔷 4. Managing Payout Schedules

#### Q12. How can a platform **control when funds are paid out** to a connected Custom account?

A) Using `balance.schedule.set()`
B) Using `payout.schedule.delay_days`
C) Set `payout_schedule` on the connected account object
D) Manually transfer each time

✅ **Answer:** C) Set `payout_schedule` on the connected account object

---

#### Q13. True or False: Platforms can override Stripe's default payout delay for Express accounts

✅ **Answer:** True

---

#### Q14. What Stripe object represents **pending funds** before payout?

A) `invoice`
B) `balance`
C) `funds_hold`
D) `payout`

✅ **Answer:** B) `balance`

---

### 🔷 5. Onboarding & Verification

#### Q15. What API is used to create a Connect account?

A) `POST /v1/customers`
B) `POST /v1/accounts`
C) `POST /v1/connect`
D) `POST /v1/users`

✅ **Answer:** B) `POST /v1/accounts`

---

#### Q16. What is the purpose of the **Account Link** object in Stripe?

A) To onboard Express users
B) To create an OAuth connection
C) To initiate account verification flows
D) To manage transfers

✅ **Answer:** C) To initiate account verification flows

---

#### Q17. True or False: You must collect all KYC documents yourself when onboarding Custom accounts

✅ **Answer:** True

---

### 🔷 6. Using Custom Accounts

#### Q18. When using Custom accounts, what responsibilities fall to the platform?

A) Customer support, refunds, KYC
B) Only initiating charges
C) Hosting payment pages
D) Nothing, Stripe handles all

✅ **Answer:** A) Customer support, refunds, KYC

---

#### Q19. How can you update the business profile for a Custom account?

A) `PATCH /v1/platforms/{id}`
B) Update the `business_profile` via `account` object
C) Use Dashboard
D) Custom accounts do not have profiles

✅ **Answer:** B) Update the `business_profile` via `account` object

---

#### Q20. True or False: With Custom accounts, you can create and manage charges entirely via your platform’s keys

✅ **Answer:** True

---

### 🔷 7. Creating Direct Charges

#### Q21. In a direct charge, what account is used to create the charge?

A) The platform
B) The connected account
C) A 3rd-party merchant
D) A virtual account

✅ **Answer:** B) The connected account

---

#### Q22. What is one limitation of direct charges?

A) Application fees cannot be collected
B) Funds settle into the platform account
C) The charge does not appear in the connected account dashboard
D) Connect must use Transfer API

✅ **Answer:** A) Application fees cannot be collected

---

#### Q23. True or False: Direct charges simplify reconciliation for platforms

✅ **Answer:** False (reconciliation is simpler with destination charges)

---

### 🔷 8. Disputes & Chargebacks

#### Q24. Who is responsible for handling a **dispute** on a direct charge?

A) The customer
B) The platform
C) The connected account
D) Stripe

✅ **Answer:** C) The connected account

---

#### Q25. Which type of charge lets the platform handle disputes and refunds?

A) Destination charge
B) Separate charge and transfer
C) Direct charge
D) Express-only charge

✅ **Answer:** A) Destination charge

---

#### Q26. True or False: Stripe automatically deducts dispute amounts from the platform’s balance in all charge types

✅ **Answer:** False (depends on who is the merchant of record)

---

### 🔷 9. Destination Charges

#### Q27. What is a key feature of **destination charges**?

A) The charge is made on the connected account
B) Platform controls payout timing, dispute handling, and funds
C) Stripe automatically transfers funds
D) Only supported on Custom accounts

✅ **Answer:** B) Platform controls payout timing, dispute handling, and funds

---

#### Q28. In a destination charge, the connected account appears as the

A) Card processor
B) Payment source
C) Merchant of record
D) Refund source

✅ **Answer:** C) Merchant of record

---

#### Q29. What parameter defines the funds flow to a connected account?

A) `platform_payout: true`
B) `destination: {account_id}`
C) `transfer_group`
D) `merchant_ref_id`

✅ **Answer:** B) `destination: {account_id}`

---

#### Q30. True or False: Destination charges allow platforms to deduct an application fee

✅ **Answer:** True

---

## ✅ API Patterns

**5% of exam** |
Demonstrate an understanding of API fundamentals, API events, webhooks, security, & testing.

### 🔐 1. API Keys

#### Q1. What is the **primary difference** between Stripe’s **publishable** and **secret** API keys?

A) Secret keys are used for UI calls
B) Publishable keys are used for server-side calls
C) Secret keys are used for server-side operations
D) Both are interchangeable

✅ **Answer:** C) Secret keys are used for server-side operations

---

#### Q2. True or False: You can safely expose your **publishable** key to the browser or client app

✅ **Answer:** True

---

#### Q3. What **best practice** should you follow for managing secret keys?

A) Hardcode in the frontend
B) Rotate regularly and store in secure environment variables
C) Store in plaintext in a database
D) Use same key across all environments

✅ **Answer:** B) Rotate regularly and store in secure environment variables

---

#### Q4. Which of the following actions **requires a secret key**?

A) Creating a Payment Element
B) Fetching payment method types
C) Creating a PaymentIntent
D) Displaying available currencies

✅ **Answer:** C) Creating a PaymentIntent

---

### 🔄 2. Expanding Responses

#### Q5. What does the **expand\[]** parameter allow you to do in the Stripe API?

A) Increase result limits
B) Return nested objects inline
C) Speed up request performance
D) Format responses as XML

✅ **Answer:** B) Return nested objects inline

---

#### Q6. When fetching a PaymentIntent, which object can be **expanded** to include details about the attached customer?

A) `expand[customer]`
B) `expand[metadata]`
C) `expand[charges]`
D) `expand[payouts]`

✅ **Answer:** A) `expand[customer]`

---

#### Q7. What is one **benefit** of using `expand[]` in a production integration?

A) Better formatting for logs
B) Eliminates the need for follow-up API calls
C) Faster webhook delivery
D) Reduces Stripe API usage

✅ **Answer:** B) Eliminates the need for follow-up API calls

---

### 🌐 3. Webhooks

#### Q8. What is the **purpose** of Stripe webhooks?

A) Secure customer payments
B) Handle fraud prevention
C) Notify your backend of asynchronous Stripe events
D) Refresh API tokens

✅ **Answer:** C) Notify your backend of asynchronous Stripe events

---

#### Q9. Which of the following is a **common webhook event**?

A) `payment_intent.succeeded`
B) `refund.created`
C) `invoice.paid`
D) All of the above

✅ **Answer:** D) All of the above

---

#### Q10. True or False: You should verify the webhook **signature** of incoming events using the Stripe webhook secret

✅ **Answer:** True

---

#### Q11. What header contains the Stripe webhook signature?

A) `X-Stripe-Webhook-Token`
B) `Authorization`
C) `Stripe-Signature`
D) `Webhook-Secret`

✅ **Answer:** C) `Stripe-Signature`

---

#### Q12. What should you do if you receive **duplicate webhook events**?

A) Ignore it
B) Check for idempotency using event `id`
C) Delete old events
D) Use it to retry failed charges

✅ **Answer:** B) Check for idempotency using event `id`

---

### ♻️ 4. Idempotent Requests

#### Q13. What is the purpose of using an **idempotency key**?

A) To repeat a request until it succeeds
B) To avoid duplicate charges when retrying API requests
C) To increase the rate limit
D) To make batch payments

✅ **Answer:** B) To avoid duplicate charges when retrying API requests

---

#### Q14. What header is used to pass an idempotency key?

A) `Stripe-Idempotency`
B) `X-Retry-ID`
C) `Idempotency-Key`
D) `Request-Repeat-Key`

✅ **Answer:** C) `Idempotency-Key`

---

#### Q15. Which types of requests **should always use** idempotency keys?

A) All `GET` requests
B) All `DELETE` requests
C) All `POST` requests that modify state (e.g., charges, refunds)
D) Stripe CLI requests only

✅ **Answer:** C) All `POST` requests that modify state (e.g., charges, refunds)

---

#### Q16. If the same idempotency key is reused with a different payload, what does Stripe do?

A) Accept both
B) Reject the second request
C) Create both objects
D) Merge the responses

✅ **Answer:** B) Reject the second request

---

### 🧪 5. Testing & Security

#### Q17. True or False: Stripe provides **test cards** and test API keys to simulate payment flows

✅ **Answer:** True

---

#### Q18. What card number simulates a successful payment in test mode?

A) `5555 5555 5555 4444`
B) `4000 0000 0000 9995`
C) `4242 4242 4242 4242`
D) `6011 0000 0000 0004`

✅ **Answer:** C) `4242 4242 4242 4242`

---

#### Q19. When testing webhooks locally, what Stripe tool is recommended?

A) `stripe run`
B) `stripe tunnel`
C) `stripe sync`
D) `stripe proxy`

✅ **Answer:** B) `stripe tunnel`

---

#### Q20. Best practice when testing payment flows in a dev environment?

A) Use real credit cards
B) Use test mode and test keys
C) Use both real and test modes
D) Disable Stripe security features

✅ **Answer:** B) Use test mode and test keys

---

## ✅ Declines, Disputes & Refunds

**10% of exam** |
Describe the challenges merchants face when dealing with declines, disputes, and refunds and discuss the ways they can reduce them using best practices and Stripe tools.

### ❌ 1. Understanding Declines and Failed Payments

#### Q1. What is a **soft decline**?

A) A charge that succeeds but is refunded
B) A temporary decline that can be retried
C) A charge that is rejected due to fraud
D) A decline due to insufficient Stripe balance

✅ **Answer:** B) A temporary decline that can be retried

---

#### Q2. What is a **hard decline**?

A) A technical failure on Stripe’s side
B) A permanent decline that should not be retried
C) A refund request from a customer
D) A decline due to network timeouts

✅ **Answer:** B) A permanent decline that should not be retried

---

#### Q3. Which of the following is a **common reason** for a card decline?

A) Incorrect CVV
B) Insufficient funds
C) Card expired
D) All of the above

✅ **Answer:** D) All of the above

---

#### Q4. True or False: Stripe retries failed payments automatically in some cases

✅ **Answer:** True

---

#### Q5. Which status indicates a **successful** charge on the PaymentIntent object?

A) `requires_action`
B) `processing`
C) `succeeded`
D) `requires_payment_method`

✅ **Answer:** C) `succeeded`

---

### 📉 2. How to Reduce Network Declines

#### Q6. What is **adaptive acceptance** in Stripe?

A) A refund strategy for failed charges
B) Stripe’s machine-learning system that selectively retries failed card payments
C) A way to accept more currencies
D) A dispute automation tool

✅ **Answer:** B) Stripe’s machine-learning system that selectively retries failed card payments

---

#### Q7. Which of these is a best practice to reduce card declines?

A) Use Payment Element
B) Send more metadata
C) Collect complete and accurate billing details
D) Skip 3D Secure

✅ **Answer:** C) Collect complete and accurate billing details

---

#### Q8. What is one reason why **automatic retries** should be used cautiously?

A) They increase authorization rates
B) They might annoy customers if too frequent
C) They reduce fraud
D) Stripe does not support retries

✅ **Answer:** B) They might annoy customers if too frequent

---

#### Q9. What Stripe feature can help **optimize authorization rates** for subscription renewals?

A) Radar
B) Smart Retries
C) Webhooks
D) Connect

✅ **Answer:** B) Smart Retries

---

#### Q10. Which API parameter can be used to request 3D Secure during a payment?

A) `require_3d_secure=true`
B) `payment_method_options[card][request_three_d_secure]`
C) `secure=true`
D) `authentication_required=manual`

✅ **Answer:** B) `payment_method_options[card][request_three_d_secure]`

---

### ⚖️ 3. Disputes & Chargebacks

#### Q11. What is a **dispute**?

A) A duplicate charge
B) A refund requested by the merchant
C) A payment challenged by a cardholder through their bank
D) A failed charge attempt

✅ **Answer:** C) A payment challenged by a cardholder through their bank

---

#### Q12. What’s the **default action** Stripe takes when a dispute is received?

A) Automatically refunds the customer
B) Ignores it
C) Deducts the disputed amount from the merchant’s balance
D) Notifies the customer

✅ **Answer:** C) Deducts the disputed amount from the merchant’s balance

---

#### Q13. What **evidence** can a merchant submit to fight a dispute?

A) Customer communication
B) Proof of delivery or service
C) Signed contracts or agreements
D) All of the above

✅ **Answer:** D) All of the above

---

#### Q14. True or False: Stripe always decides the outcome of a dispute

✅ **Answer:** False — The issuing bank decides the outcome.

---

#### Q15. Which Stripe API object contains dispute details?

A) `dispute_object`
B) `Charge.dispute`
C) `Refund.dispute_info`
D) `PaymentIntent.dispute_summary`

✅ **Answer:** B) `Charge.dispute`

---

### 💸 4. Refunds & Fraud Prevention

#### Q16. What is a **refund**?

A) A chargeback initiated by Stripe
B) A manual reversal of a successful payment
C) An automatic failure
D) An alert triggered by Radar

✅ **Answer:** B) A manual reversal of a successful payment

---

#### Q17. Which parameter must be passed to **issue a refund** via the Stripe API?

A) `transaction_id`
B) `payment_method`
C) `charge`
D) `dispute_id`

✅ **Answer:** C) `charge`

---

#### Q18. What’s one way to **prevent friendly fraud** (e.g., customers claiming they didn’t authorize a legit charge)?

A) Skip 3D Secure
B) Use Radar with rules
C) Don’t send receipts
D) Avoid using email

✅ **Answer:** B) Use Radar with rules

---

#### Q19. True or False: You can partially refund a charge via the Stripe Dashboard or API

✅ **Answer:** True

---

#### Q20. What Stripe tool helps merchants reduce fraud **before** a transaction occurs?

A) Dispute dashboard
B) Radar
C) Billing Portal
D) Adaptive payouts

✅ **Answer:** B) Radar

---

## ✅ Reporting & Reconciliation

**5% of exam** |
Describe the reports a merchant should use to solve a given business need and identify typical reconciliation tasks a merchant might take using Stripe.

### **1. Which Stripe report is most appropriate for reconciling individual charges to payouts?**

A. Disputes Report
B. Balance Summary Report
C. Payout Reconciliation Report
D. Payment Summary Report

✅ **Correct Answer: C**

---

### **2. What does the Payout Reconciliation Report help merchants determine?**

A. The breakdown of international transaction fees
B. How each transaction in Stripe maps to a specific payout
C. Chargeback win rate over time
D. Subscription lifecycle stages

✅ **Correct Answer: B**

---

### **3. A merchant needs to report gross and net revenue on a monthly basis. Which report should they use?**

A. Balance History Report
B. Financial Reports > Monthly Reports
C. Radar Fraud Report
D. Account Summary Report

✅ **Correct Answer: B**

---

### **4. Which balance transaction type would represent a successful charge on a card?**

A. `charge.refund`
B. `payout`
C. `charge`
D. `transfer`

✅ **Correct Answer: C**

---

### **5. What balance transaction type represents a fee charged by Stripe?**

A. `fee`
B. `charge.fee`
C. `stripe_fee`
D. `application_fee`

✅ **Correct Answer: D**

---

### **6. When reconciling across currencies, what does Stripe use to handle conversions?**

A. Real-time forex market rates
B. The conversion rate at the time of the payout
C. The conversion rate at the time of the charge
D. The merchant’s bank rate

✅ **Correct Answer: B**

---

### **7. Which report includes data needed to reconcile Stripe fees at the transaction level?**

A. Tax Summary Report
B. Dispute Report
C. Balance Transaction Report
D. Conversion Rate Report

✅ **Correct Answer: C**

---

### **8. A merchant notices a mismatch between expected and actual payout amounts. What should be checked first?**

A. Tax settings
B. Balance transactions associated with the payout
C. Customer email addresses
D. Number of subscriptions

✅ **Correct Answer: B**

---

### **9. What type of transaction would you expect to see when a charge is refunded in full?**

A. `charge`
B. `refund`
C. `charge.refund`
D. `adjustment`

✅ **Correct Answer: C**

---

### **10. What is the purpose of the Balance Summary Report?**

A. To summarize fraud outcomes
B. To summarize all activity affecting your Stripe balance
C. To analyze churn
D. To review integration errors

✅ **Correct Answer: B**

---

### **11. Which of the following would NOT typically appear in a Stripe financial report?**

A. Chargebacks
B. Invoice payments
C. Staff payroll data
D. Currency conversion rates

✅ **Correct Answer: C**

---

### **12. Where can a merchant find a detailed breakdown of gross volume, fees, and net volume by day?**

A. Radar Dashboard
B. Financial Reports > Daily Summaries
C. Customer Portal
D. Connect Account Overview

✅ **Correct Answer: B**

---

### **13. Which of the following tasks is essential for reconciliation in a multi-currency account?**

A. Comparing bank fees across providers
B. Matching payout amounts with exchange-adjusted transactions
C. Checking user logs
D. Verifying webhook retry attempts

✅ **Correct Answer: B**

---

### **14. What’s a common use for Stripe’s “Report Types Reference”?**

A. To understand fraud patterns
B. To identify webhook performance
C. To find definitions and schema for downloadable Stripe reports
D. To troubleshoot failed payments

✅ **Correct Answer: C**

---

### **15. Which report should a merchant consult to verify the total fees collected by Stripe in a billing cycle?**

A. Tax Report
B. Dispute Summary
C. Monthly Financial Report
D. Issuing Transactions Report

✅ **Correct Answer: C**

---

### **16. Why might the net balance in a payout differ from gross collected charges?**

A. Delays in bank settlements
B. Unverified accounts
C. Stripe fees, refunds, and disputes
D. Expired cards

✅ **Correct Answer: C**

---

### **17. A business using Stripe Connect wants to reconcile funds paid out to connected accounts. Which tool is best?**

A. Account Summary
B. Connect Transfers Report
C. Issuing Reconciliation Report
D. Invoices by Period Report

✅ **Correct Answer: B**

---

### **18. What does Stripe require to verify account identity before enabling payouts?**

A. Customer phone numbers
B. Full tax reports
C. Government-issued documentation and business information
D. Shipping labels

✅ **Correct Answer: C**

---

### **19. How frequently are Stripe’s standard financial reports generated?**

A. Real-time only
B. Daily and Monthly
C. Quarterly
D. Weekly only

✅ **Correct Answer: B**

---

### **20. A merchant wants to reconcile subscription payments by invoice. Which report or method should they use?**

A. Radar Logs
B. Webhook Event Logs
C. Invoice Line Item Export
D. Conversion Funnel Report

✅ **Correct Answer: C**

---

## ✅ Global Business & Compliance

 **5% of exam** |
Describe the common issues a global business will face when using Stripe to accept payments and move money between accounts including foreign exchange, cross-border transactions, and common payment methods.

### **1. What challenge does foreign exchange (FX) present to global businesses using Stripe?**

A. It increases the number of chargebacks.
B. It can lead to currency conversion losses and affect reconciliation.
C. It eliminates the need for Know Your Customer (KYC) checks.
D. It simplifies payout reconciliation.
✅ **Correct Answer: B**

---

### **2. When a business accepts a payment in one currency and receives the payout in another, what does Stripe apply?**

A. International settlement
B. Dual-invoice adjustment
C. Currency conversion using Stripe’s FX rate
D. Local banking override

✅ **Correct Answer: C**

---

### **3. What is a typical concern when moving money between accounts across borders using Stripe?**

A. Insufficient tax reporting
B. Regulatory restrictions on cross-border payouts
C. Slower webhook delivery
D. Customer verification delays

✅ **Correct Answer: B**

---

### **4. Which payment method is MOST likely to be used by customers in Europe?**

A. ACH
B. FPX
C. SEPA Direct Debit
D. OXXO

✅ **Correct Answer: C**

---

### **5. What is the main purpose of the **Integration Security Guide** provided by Stripe?**

A. To teach users how to build dashboards
B. To offer guidance on regulatory licensing
C. To help secure payment integrations and protect sensitive data
D. To debug webhook failures

✅ **Correct Answer: C**

---

### **6. Why might a global business choose to use **multiple bank accounts** in Stripe?**

A. To isolate disputes
B. To increase payment method acceptance
C. To handle local currency payouts in multiple regions
D. To link multiple customer accounts

✅ **Correct Answer: C**

---

### **7. Which of the following is **not** a supported strategy to reduce FX and cross-border fees in Stripe?**

A. Enable multi-currency payouts
B. Localize bank accounts for key markets
C. Set all charges to USD regardless of location
D. Match the currency of charges to customer location

✅ **Correct Answer: C**

---

### **8. What is a benefit of using Stripe Connect for global platforms?**

A. Automatically handles tax reporting
B. Simplifies international verification and fund flows
C. Guarantees faster refunds
D. Eliminates dispute risk

✅ **Correct Answer: B**

---

### **9. Which method would help a merchant stay compliant with local regulations when operating internationally?**

A. Using localized payment methods
B. Issuing one invoice per country
C. Turning off charge notifications
D. Forcing customers to pay in the platform's home currency

✅ **Correct Answer: A**

---

### **10. What is a **risk** associated with cross-border fund transfers?**

A. Double entry in the dashboard
B. Outdated webhook formats
C. Noncompliance with local tax or anti-money laundering laws
D. Duplicate customer creation

✅ **Correct Answer: C**

---

### **11. A business using Stripe wants to allow customers in Brazil to pay with cash. Which method should be supported?**

A. Boleto Bancário
B. SEPA
C. ACH Debit
D. WeChat Pay

✅ **Correct Answer: A**

---

### **12. Which of the following ensures that Stripe merchants are complying with **Know Your Customer (KYC)** requirements?**

A. Two-factor authentication
B. Completing the Stripe identity verification process
C. Providing Apple Pay certificates
D. Enabling Instant Payouts

✅ **Correct Answer: B**

---

### **13. What is one **security practice** recommended in the Stripe Integration Security Guide?**

A. Embed secret keys in frontend code for easy access
B. Use test API keys in production
C. Use webhooks with signature verification
D. Avoid TLS for internal systems

✅ **Correct Answer: C**

---

### **14. What is the benefit of using local acquiring via Stripe in multiple regions?**

A. Faster onboarding
B. Access to more test data
C. Higher conversion rates and fewer declined transactions
D. Lower refund percentages

✅ **Correct Answer: C**

---

### **15. Which of the following payment methods is specific to the **Asia-Pacific** region?**

A. iDEAL
B. FPX
C. Bacs Direct Debit
D. ACH Credit

✅ **Correct Answer: B**

---

### **16. Why should a global platform implement fraud controls like Stripe Radar when expanding internationally?**

A. To automate onboarding
B. To reduce network latency
C. To adapt to different fraud patterns and regulatory requirements
D. To manage employee access

✅ **Correct Answer: C**

---

### **17. What happens if a Stripe account is not properly verified for payouts?**

A. Payments are automatically refunded
B. Payouts are delayed or blocked
C. Payments are charged double
D. The account is removed from Radar

✅ **Correct Answer: B**

---

### **18. How does Stripe handle FX fees for international payments?**

A. Charges a flat \$1 fee for all FX
B. Includes FX fees in Stripe’s displayed conversion rate
C. Uses bank-provided rates with added markup
D. Sends the fee separately via a webhook

✅ **Correct Answer: B**

---

### **19. Why might a merchant want to restrict payment methods by region in Stripe?**

A. To reduce webhook load
B. To limit customer refunds
C. To prevent unsupported methods for certain countries
D. To increase chargeback risk

✅ **Correct Answer: C**

---

### **20. A business operating in the EU and US wants to separate its funds for regulatory reasons. What Stripe feature is most appropriate?**

A. Smart Retries
B. Stripe Tax
C. Multiple Bank Accounts per country
D. Payment Links

✅ **Correct Answer: C**

---

## ✅ Payment Methods

**10% of exam** |
Demonstrate an understanding of common payment methods used by Stripe users in North America and Europe.  

### **1. Which payment method is commonly used in the United States for direct bank payments?**

A. SEPA Direct Debit
B. ACH Debit
C. iDEAL
D. FPX

✅ **Correct Answer: B**

---

### **2. A customer in the Netherlands prefers to pay via online banking. Which method should the merchant offer?**

A. Boleto
B. Klarna
C. iDEAL
D. Bancontact

✅ **Correct Answer: C**

---

### **3. What is a **Payment Link** in Stripe?**

A. A one-time API token to accept subscriptions
B. A reusable, no-code link to collect payment via a Stripe-hosted checkout page
C. A webhook event for manual payment collection
D. A QR code generator

✅ **Correct Answer: B**

---

### **4. What type of payment method typically supports **delayed settlement**?**

A. Card payments
B. ACH and SEPA bank debits
C. Apple Pay
D. Google Pay

✅ **Correct Answer: B**

---

### **5. Which European payment method allows installment-based purchases?**

A. iDEAL
B. Klarna
C. FPX
D. ACH Credit

✅ **Correct Answer: B**

---

### **6. What happens when you **place a hold** on a payment method using Stripe?**

A. Stripe immediately charges the customer
B. Funds are authorized but not captured until later
C. Payment method is removed from the customer object
D. Funds are converted to the merchant’s local currency

✅ **Correct Answer: B**

---

### **7. Which of the following payment methods supports **real-time confirmation** of successful payments?**

A. ACH Credit Transfer
B. SEPA Direct Debit
C. Cards
D. Boleto

✅ **Correct Answer: C**

---

### **8. What should a business consider when choosing a payment method to support with Stripe?**

A. The default locale of the Stripe Dashboard
B. Customer region and payment preferences
C. The account owner’s language settings
D. Whether webhook retries are enabled

✅ **Correct Answer: B**

---

### **9. What is the main benefit of using **bank transfers** via Stripe?**

A. Instant settlement
B. No reconciliation is needed
C. High-value transactions with lower fees
D. Fully refundable transactions only

✅ **Correct Answer: C**

---

### **10. What does Stripe recommend when accepting bank transfers from customers?**

A. Avoid displaying bank account details
B. Assign a virtual bank account or reference to each customer
C. Only accept transfers from card networks
D. Use separate accounts for each currency

✅ **Correct Answer: B**

---

### **11. A business wants to let customers pay without entering card details. Which method would be appropriate?**

A. Google Pay
B. Card tokenization
C. Instant Payouts
D. Smart Retries

✅ **Correct Answer: A**

---

### **12. What happens if a payment using a **Payment Link** fails due to insufficient funds?**

A. The link is automatically disabled
B. Stripe retries automatically based on retry logic
C. Stripe refunds the previous transaction
D. The link generates a new customer object

✅ **Correct Answer: B**

---

### **13. A Stripe merchant wants to sell in Germany and offer a widely used **debit** payment method. What should they enable?**

A. Bancontact
B. SEPA Direct Debit
C. Przelewy24
D. OXXO

✅ **Correct Answer: B**

---

### **14. What’s a common reason for delayed confirmation in **ACH payments**?**

A. Currency mismatch
B. Manual review by Stripe
C. The need to complete micro-deposit verification
D. Use of an expired API key

✅ **Correct Answer: C**

---

### **15. Which payment method is designed specifically for customers in Belgium?**

A. SEPA
B. FPX
C. Bancontact
D. Alipay

✅ **Correct Answer: C**

---

### **16. What should merchants include when requesting bank transfer payments using Stripe?**

A. A signed agreement
B. The customer’s physical address
C. Unique reference codes per transaction
D. Manual reconciliation processes

✅ **Correct Answer: C**

---

### **17. Why might a business choose to use **Payment Links** instead of building a custom checkout flow?**

A. To avoid PCI compliance
B. To allow payments with offline capture
C. For speed, simplicity, and no-code deployment
D. To reduce transaction fees

✅ **Correct Answer: C**

---

### **18. What does **Learn about payment methods** documentation on Stripe provide?**

A. Payment processor comparison charts
B. Regional availability, customer experience, and compatibility for each method
C. CSV templates for importing customers
D. A fee calculator

✅ **Correct Answer: B**

---

### **19. What feature lets a merchant **authorize** a card payment now and **capture** it later?**

A. Delayed settlement override
B. PaymentIntent with manual capture
C. Transfer reversal
D. CaptureMode API

✅ **Correct Answer: B**

---

### **20. A user wants to accept Bacs Direct Debit in the UK. What should they be aware of?**

A. Instant confirmation and same-day settlement
B. Longer confirmation times and potential for failed debits
C. Automatic tax calculation
D. Mandatory Payment Links

✅ **Correct Answer: B**

---

## ✅ Using Radar & Reducing Fraud

**10% of exam** |
Demonstrate an understanding of the types of fraud a Stripe user may experience and how to use Radar and Radar for Fraud Teams to reduce fraud.

### **1. What type of fraud is most common in online card payments?**

A. Inventory fraud
B. Account takeover
C. Card-not-present (CNP) fraud
D. Fake refund fraud

✅ **Correct Answer: C**

---

### **2. What is the purpose of Stripe Radar?**

A. To handle disputes and chargebacks
B. To evaluate and block potentially fraudulent transactions in real time
C. To calculate exchange rates for international payments
D. To automate invoice generation

✅ **Correct Answer: B**

---

### **3. What is the default action Stripe Radar takes on high-risk payments?**

A. Immediately refunds the charge
B. Declines the payment
C. Escalates to the merchant
D. Routes to manual review

✅ **Correct Answer: B**

---

### **4. What score does Stripe Radar assign to every transaction to evaluate risk?**

A. Payment Strength Index
B. Risk Score (0.0 to 1.0)
C. Radar Alert Level
D. Stripe Confidence Metric

✅ **Correct Answer: B**

---

### **5. What does a Radar risk score of 0.95 indicate?**

A. The payment has a very low chance of being fraud
B. The payment is 95% compliant with 3DS
C. The payment is likely fraudulent
D. The customer has a strong spending history

✅ **Correct Answer: C**

---

### **6. What is a Radar rule used for?**

A. Adjusting tax rates on international transactions
B. Customizing fraud detection behavior, such as blocking or reviewing payments
C. Determining FX fees
D. Reversing transfers to connected accounts

✅ **Correct Answer: B**

---

### **7. Which of the following is **not** a feature of **Radar for Fraud Teams**?**

A. Custom rule creation
B. Block/allow lists
C. Risk insights and analytics
D. Chargeback automation for physical goods

✅ **Correct Answer: D**

---

### **8. What’s the benefit of Radar’s **device fingerprinting**?**

A. Improves shipping accuracy
B. Verifies customer age
C. Helps detect unusual patterns tied to specific browsers or devices
D. Encrypts customer payment info

✅ **Correct Answer: C**

---

### **9. When should a business consider **manually reviewing** a payment in Radar?**

A. When it's below the minimum risk threshold
B. When it triggers multiple risk signals but isn't clearly fraudulent
C. If the payment was completed via bank transfer
D. If it includes a coupon code

✅ **Correct Answer: B**

---

### **10. What is a common **false positive** in fraud detection?**

A. A dispute that wins automatically
B. A legitimate transaction flagged as fraudulent
C. A card charge that times out
D. A failed webhook attempt

✅ **Correct Answer: B**

---

### **11. Which of the following signals can Radar use for evaluating payment risk?**

A. Card issuing bank's URL
B. Customer's birth date
C. IP address and geolocation
D. Coupon expiration date

✅ **Correct Answer: C**

---

### **12. What’s one way to reduce friction for **legitimate customers** while maintaining fraud protection?**

A. Set all Radar rules to “block”
B. Use allow lists for known customer emails or card fingerprints
C. Disable webhook validation
D. Increase the payment timeout period

✅ **Correct Answer: B**

---

### **13. What is the **primary difference** between Stripe Radar and Radar for Fraud Teams?**

A. Radar only works for Connect accounts
B. Radar for Fraud Teams includes advanced tools like custom rules and review queues
C. Radar is a paid upgrade while Fraud Teams is free
D. Radar for Fraud Teams supports only US cards

✅ **Correct Answer: B**

---

### **14. A merchant wants to block payments from a specific country. What Radar feature should they use?**

A. Risk Thresholds
B. Device Watchlists
C. Radar Rule with `ip_country` condition
D. Delay capture API

✅ **Correct Answer: C**

---

### **15. Why would a payment flagged with a **risk level of “elevated”** not be automatically blocked?**

A. It has already been refunded
B. The customer has a saved card
C. The account’s Radar rules are set to allow elevated risk
D. The card supports 3DS

✅ **Correct Answer: C**

---

### **16. What can you do if a transaction is mistakenly **blocked** by Radar?**

A. Reverse the charge using the dashboard
B. Create a new API key
C. Add the customer or card to the allow list and retry the payment
D. Re-run the webhook event

✅ **Correct Answer: C**

---

### **17. What is a **benefit of using Radar’s machine learning** model?**

A. Requires no internet connection
B. Only works with Stripe Terminal
C. Continuously improves using global fraud data
D. Works exclusively on subscription payments

✅ **Correct Answer: C**

---

### **18. How often is Stripe’s Radar model retrained?**

A. Every year
B. Every 24 hours
C. Continuously with new data
D. Only during fraud spikes

✅ **Correct Answer: C**

---

### **19. What does Stripe’s **Radar Dashboard** allow a business to do?**

A. Run payouts manually
B. Access all webhook logs
C. Review blocked, allowed, and reviewed payments
D. Generate monthly reconciliation reports

✅ **Correct Answer: C**

---

### **20. What’s a **best practice** when writing custom rules in Radar?**

A. Use only `email` as a condition
B. Combine multiple risk signals to reduce false positives
C. Allow all payments under \$10
D. Disable 3D Secure

✅ **Correct Answer: B**
