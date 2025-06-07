# 🧠 **Stripe Associate Architect Certification

## Sample Paper 3 (with Answers)**

### ✅ Payments (20% – 10 Questions)

1. **Which API should you use to create a one-time card payment while supporting regulatory compliance such as 3D Secure?**
   A. Charges API
   B. Setup Intents API
   C. Payment Intents API
   D. Customer API
   **✔️ Answer: C**

2. **What is the main advantage of using the Payment Element in a frontend integration?**
   A. It supports bank transfers only
   B. It only works in Europe
   C. It provides a pre-built, secure UI for collecting payment method details
   D. It avoids PCI compliance entirely
   **✔️ Answer: C**

3. **Which object represents a successful movement of funds from a customer to your Stripe account?**
   A. Transfer
   B. Balance Transaction
   C. PaymentIntent
   D. Charge
   **✔️ Answer: D**

4. **Which method allows you to support different currencies across multiple countries?**
   A. Use only USD in all transactions
   B. Create separate accounts for each country
   C. Specify the currency in the `amount` object of the PaymentIntent
   D. Set the currency in your Dashboard
   **✔️ Answer: C**

5. **To receive payouts, what Stripe object must a platform or user have?**
   A. Transfer object
   B. Customer object
   C. External Account (Bank Account or Debit Card)
   D. PaymentIntent
   **✔️ Answer: C**

6. **Which Stripe feature handles Strong Customer Authentication (SCA)?**
   A. Radar
   B. Payment Element
   C. SetupIntent
   D. 3D Secure via Payment Intents
   **✔️ Answer: D**

7. **Which API object allows you to handle failed payments and retries in subscription billing?**
   A. Invoice
   B. Charge
   C. PaymentIntent
   D. Subscription
   **✔️ Answer: A**

8. **What happens if the `currency` of a PaymentIntent is not supported by the customer’s payment method?**
   A. Stripe will automatically convert it
   B. The transaction will fail
   C. Stripe will suggest a valid currency
   D. It is up to the platform to handle
   **✔️ Answer: B**

9. **Which endpoint allows you to retrieve a full list of previous payouts?**
   A. `GET /v1/transfers`
   B. `GET /v1/payouts`
   C. `GET /v1/charges`
   D. `GET /v1/balance_transactions`
   **✔️ Answer: B**

10. **Which object is responsible for initiating the payment in Stripe's modern flow?**
    A. SetupIntent
    B. PaymentIntent
    C. Source
    D. Transfer
    **✔️ Answer: B**

---

### ✅ Billing (10% – 5 Questions)

11. **What’s the primary benefit of using Stripe Billing for a SaaS platform?**
    A. Faster payouts
    B. PCI compliance
    C. Easily managing recurring payments and subscriptions
    D. Automatic chargebacks
    **✔️ Answer: C**

12. **Which pricing model is best for metered usage?**
    A. Flat pricing
    B. Tiered pricing
    C. Per-seat pricing
    D. Usage-based pricing
    **✔️ Answer: D**

13. **Which object must be created first in order to create a subscription?**
    A. PaymentIntent
    B. Customer
    C. Product
    D. Invoice
    **✔️ Answer: C**

14. **What happens when a subscription is downgraded mid-cycle?**
    A. The user loses all features immediately
    B. The invoice is voided
    C. Prorations are calculated automatically
    D. No changes until next billing cycle
    **✔️ Answer: C**

15. **Which Stripe guide focuses on avoiding issues that can affect authorization rates?**
    A. PCI Guide
    B. Integration Security Guide
    C. Billing Optimization Guide
    D. Platform Setup Guide
    **✔️ Answer: B**

---

### ✅ Connect (15% – 8 Questions)

16. **Which Connect account type gives you full control over the user experience?**
    A. Standard
    B. Express
    C. Custom
    D. Basic
    **✔️ Answer: C**

17. **What’s the difference between a `separate charge and transfer` and a `destination charge`?**
    A. They are the same
    B. Separate charge and transfer splits charge and payout; destination charge handles it in one step
    C. Destination charge uses a third-party processor
    D. Separate charges are for international payments only
    **✔️ Answer: B**

18. **Which Connect account type provides a Stripe-hosted onboarding flow?**
    A. Custom
    B. Express
    C. Standard
    D. Lite
    **✔️ Answer: B**

19. **What object is required for managing onboarding for a Custom account?**
    A. AccountToken
    B. SetupIntent
    C. AccountLink
    D. Express URL
    **✔️ Answer: C**

20. **How can platforms customize the payout schedule for Connect accounts?**
    A. Through the Dashboard only
    B. Using the `payout_schedule` parameter in the account object
    C. By manually writing to the account's ledger
    D. Not supported
    **✔️ Answer: B**

21. **Which method allows you to create a charge on behalf of a connected account while the platform handles risk and refunds?**
    A. Standard charge
    B. Destination charge
    C. Separate charge and transfer
    D. Direct charge
    **✔️ Answer: B**

22. **What triggers a dispute process in Stripe?**
    A. A declined payment
    B. A manual refund
    C. A customer contacting their bank to reverse a charge
    D. A failed webhook
    **✔️ Answer: C**

23. **How can you view funds flow in Connect transactions?**
    A. Through the Transfers API
    B. Balance Transaction API
    C. Connect dashboard with reporting
    D. All of the above
    **✔️ Answer: D**

---

### ✅ API Patterns (5% – 3 Questions)

24. **What is the purpose of idempotency in Stripe API requests?**
    A. Prevent duplicate webhooks
    B. Enable retries without duplication
    C. Prevent refund
    D. Cancel transactions
    **✔️ Answer: B**

25. **What is an expanded response in Stripe APIs?**
    A. A cached version of response
    B. An error message
    C. Including nested resources in the API response
    D. An extended timeout
    **✔️ Answer: C**

26. **Which method verifies that your webhook endpoint receives Stripe events securely?**
    A. IP address allowlisting
    B. Shared secret signing
    C. TLS v1.0 encryption
    D. API keys
    **✔️ Answer: B**

---

### ✅ Declines, Disputes & Refunds (10% – 5 Questions)

27. **What is a common cause of hard declines?**
    A. Bank timeout
    B. Incorrect CVV or card number
    C. Temporary downtime
    D. Duplicate charge
    **✔️ Answer: B**

28. **How can a merchant reduce network declines?**
    A. Retry all payments
    B. Use outdated tokens
    C. Use Stripe’s Smart Retries
    D. Disable fraud detection
    **✔️ Answer: C**

29. **Which tool helps fight fraud in real-time?**
    A. Express onboarding
    B. Radar
    C. Connect
    D. Payment Links
    **✔️ Answer: B**

30. **What is the best action after receiving a legitimate dispute?**
    A. Immediately refund
    B. Provide evidence through Stripe Dashboard
    C. Contact customer manually
    D. Re-charge the card
    **✔️ Answer: B**

31. **What’s a good practice to reduce fraudulent charges?**
    A. Disable 3DS
    B. Use manual authorization
    C. Use Radar Rules and Risk Scoring
    D. Always retry declines
    **✔️ Answer: C**

---

### ✅ Reporting & Reconciliation (5% – 3 Questions)

32. **Which report helps reconcile payouts with Stripe balance transactions?**
    A. Dispute report
    B. Payout Reconciliation report
    C. Refund Summary
    D. Invoice overview
    **✔️ Answer: B**

33. **Which type of report is best for accounting and general ledger entries?**
    A. Balance report
    B. Financial reports
    C. Radar logs
    D. Transfer summaries
    **✔️ Answer: B**

34. **What’s included in a balance transaction object?**
    A. Description only
    B. Currency only
    C. Amount, fee, type, and available\_on
    D. Refund reason
    **✔️ Answer: C**

---

### ✅ Global Business & Compliance (5% – 3 Questions)

35. **What is a key compliance consideration for cross-border payments?**
    A. Use only USD
    B. Comply with KYC and AML regulations
    C. Use manual payouts
    D. Avoid verification
    **✔️ Answer: B**

36. **How does Stripe handle currency conversion?**
    A. It requires manual conversion
    B. Stripe automatically converts at the current rate with a small fee
    C. Stripe uses PayPal to convert
    D. It is not supported
    **✔️ Answer: B**

37. **Why might a business use multiple bank accounts in Stripe?**
    A. For load balancing
    B. For faster payments
    C. To route payouts per currency
    D. To avoid fees
    **✔️ Answer: C**

---

### ✅ Payment Methods (10% – 5 Questions)

38. **What is the purpose of a Payment Link?**
    A. To store card info
    B. To accept payments without writing any code
    C. To issue refunds
    D. To trigger a webhook
    **✔️ Answer: B**

39. **Which method is commonly used for business payments in Europe?**
    A. UPI
    B. Klarna
    C. ACH
    D. Card-only
    **✔️ Answer: B**

40. **How can you enable a bank transfer payment in Stripe?**
    A. Manually ask customer for payment
    B. Enable via Dashboard or API for supported currencies
    C. Only via Express accounts
    D. By disabling card payments
    **✔️ Answer: B**

41. **How can a platform place a hold on a card without charging it immediately?**
    A. Using `PaymentIntent` with `capture_method: manual`
    B. Using `Charge` API
    C. By delaying invoice creation
    D. Stripe doesn’t support this
    **✔️ Answer: A**

42. **Which payment method is preferred for recurring billing in Europe?**
    A. Credit Cards
    B. Klarna
    C. SEPA Direct Debit
    D. PayNow
    **✔️ Answer: C**

---

### ✅ Radar & Reducing Fraud (10% – 5 Questions)

43. **What does Radar use to evaluate fraud risk?**
    A. Manual scoring
    B. Machine learning on global network
    C. Card expiration
    D. Dashboard settings
    **✔️ Answer: B**

44. **What’s a best practice for reducing chargebacks?**
    A. Disable Radar
    B. Enable 3D Secure
    C. Accept all payments
    D. Ignore declines
    **✔️ Answer: B**

45. **Which of the following can Radar Rules do?**
    A. Export CSV
    B. Block specific countries or email domains
    C. Create invoices
    D. Adjust payout frequency
    **✔️ Answer: B**

46. **What is Radar for Fraud Teams?**
    A. A set of JavaScript tools
    B. A premium Radar plan with advanced rules and reporting
    C. A payment gateway
    D. A support tool
    **✔️ Answer: B**

47. **What is a benefit of Risk Evaluation in Stripe?**
    A. Automatically delays payouts
    B. Helps make authorization decisions
    C. Deletes customer data
    D. Hides payment methods
    **✔️ Answer: B**
