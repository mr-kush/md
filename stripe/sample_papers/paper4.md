# 🧪 **Stripe Associate Architect Certification – Sample Paper 4 (with Answers)**

---

## ✅ Payments (20% – 10 Questions)

1. **Which API allows merchants to comply with regulations like PSD2 and supports authentication steps such as 3D Secure?**
   A. Charges API
   B. Payment Intents API
   C. Setup Intents API
   D. Transfer API
   **✔️ Answer: B**

2. **What does the `status: requires_action` on a PaymentIntent indicate?**
   A. The payment has succeeded
   B. A retry is required
   C. Further authentication (e.g., 3DS) is needed
   D. The customer object is missing
   **✔️ Answer: C**

3. **What is the key role of the Payment Element?**
   A. Manually creates charges
   B. Handles authentication challenges
   C. Provides a customizable UI to accept multiple payment methods
   D. Sends emails to customers
   **✔️ Answer: C**

4. **How do you hold funds on a card without capturing them immediately?**
   A. Use `setup_future_usage` on PaymentIntent
   B. Set `capture_method: manual` on PaymentIntent
   C. Use a Source object
   D. Use Checkout Session
   **✔️ Answer: B**

5. **What triggers the creation of a Charge object when using the PaymentIntents API?**
   A. When PaymentIntent is confirmed
   B. When SetupIntent is created
   C. When a refund is requested
   D. On customer creation
   **✔️ Answer: A**

6. **Which method is suitable for future off-session payments?**
   A. PaymentIntent
   B. SetupIntent
   C. Payout
   D. Transfer
   **✔️ Answer: B**

7. **What is a possible reason for a payment failure despite a successful charge creation?**
   A. Charge object was invalid
   B. 3D Secure failed
   C. Customer wasn't created
   D. Incorrect webhooks
   **✔️ Answer: B**

8. **Which Stripe object represents actual money movement in the account?**
   A. Product
   B. Balance transaction
   C. Subscription
   D. Session
   **✔️ Answer: B**

9. **How does Stripe handle unsupported currencies for the merchant’s default bank account?**
   A. It rejects the payment
   B. It automatically converts the currency
   C. It asks the customer to convert
   D. It defaults to USD
   **✔️ Answer: B**

10. **Which object helps retrieve all charges and payments for accounting?**
    A. Subscription
    B. Charge
    C. PaymentIntent
    D. Balance Transaction
    **✔️ Answer: D**

---

## ✅ Billing (10% – 5 Questions)

11. **Which billing model is ideal for SaaS companies with fixed pricing tiers?**
    A. Metered billing
    B. Flat-rate subscription
    C. Per-seat billing
    D. Usage-based billing
    **✔️ Answer: B**

12. **What does Stripe generate when a subscription period ends?**
    A. Refund
    B. Webhook
    C. Invoice
    D. Payout
    **✔️ Answer: C**

13. **Which object links a customer to a subscription plan?**
    A. Product
    B. Plan
    C. Customer
    D. Subscription
    **✔️ Answer: D**

14. **Which API allows automatic proration when updating a subscription mid-cycle?**
    A. `POST /v1/charges`
    B. `POST /v1/subscriptions`
    C. `POST /v1/invoices`
    D. `GET /v1/products`
    **✔️ Answer: B**

15. **What is the role of metered billing in Stripe?**
    A. It charges a fixed amount
    B. It allows custom payment links
    C. It calculates charges based on usage reports
    D. It enables multi-currency support
    **✔️ Answer: C**

---

## ✅ Connect (15% – 8 Questions)

16. **What type of Connect account gives platforms full control over UI and user experience?**
    A. Standard
    B. Express
    C. Custom
    D. External
    **✔️ Answer: C**

17. **Which Connect account type redirects users to a Stripe-hosted onboarding flow?**
    A. Express
    B. Custom
    C. Standard
    D. White-label
    **✔️ Answer: A**

18. **Which feature allows a platform to take an application fee from a transaction?**
    A. SetupIntent
    B. Destination charge
    C. Application\_fee\_amount
    D. Risk evaluation
    **✔️ Answer: C**

19. **How does a destination charge work?**
    A. The platform creates and keeps the charge
    B. The connected account receives funds; platform manages the charge
    C. The connected account creates the charge
    D. It is used for international payouts
    **✔️ Answer: B**

20. **Which flow allows the platform to handle compliance and risk entirely?**
    A. Express
    B. Custom
    C. Standard
    D. Hosted
    **✔️ Answer: B**

21. **Which object is used for creating an onboarding link for a connected account?**
    A. SetupIntent
    B. AccountLink
    C. Session
    D. AccountToken
    **✔️ Answer: B**

22. **What is required to enable payouts for a Connect account?**
    A. 2FA
    B. Verification information and external account
    C. Email confirmation
    D. Smart retries
    **✔️ Answer: B**

23. **Which report helps you understand fund movement across Connect accounts?**
    A. Transfer Report
    B. Payout Reconciliation Report
    C. Financial Report
    D. Application Fee Report
    **✔️ Answer: A**

---

## ✅ API Patterns (5% – 3 Questions)

24. **What does an idempotency key prevent?**
    A. Overuse of API
    B. Duplicate operations in case of retries
    C. Unauthorized requests
    D. Webhook spam
    **✔️ Answer: B**

25. **What’s the purpose of `expand[]` in Stripe API calls?**
    A. Avoid pagination
    B. Retry failed requests
    C. Include nested objects in the response
    D. Reduce latency
    **✔️ Answer: C**

26. **What’s the best way to ensure secure webhook delivery?**
    A. Use HTTPS
    B. Enable Radar
    C. Use webhook secret signature verification
    D. Whitelist IPs
    **✔️ Answer: C**

---

## ✅ Declines, Disputes & Refunds (10% – 5 Questions)

27. **What is the best way to avoid hard declines?**
    A. Retry every 5 seconds
    B. Update card tokens
    C. Collect accurate card details
    D. Disable CVV
    **✔️ Answer: C**

28. **What tool helps platforms reduce fraud and avoid disputes?**
    A. Smart Retries
    B. Radar
    C. Connect
    D. Payment Element
    **✔️ Answer: B**

29. **What causes a soft decline?**
    A. Invalid CVV
    B. Card limit exceeded
    C. Card lost or stolen
    D. Temporary technical issue or authentication required
    **✔️ Answer: D**

30. **What is the most appropriate response to a fraudulent charge?**
    A. Block user
    B. Wait and retry
    C. Submit Radar evidence
    D. Submit dispute evidence or refund
    **✔️ Answer: D**

31. **Which Stripe setting increases authorization success and reduces declines?**
    A. Delay invoices
    B. Enable Smart Retries and dynamic authentication
    C. Increase fees
    D. Enable test mode
    **✔️ Answer: B**

---

## ✅ Reporting & Reconciliation (5% – 3 Questions)

32. **Which report gives a summary of fees and net amounts?**
    A. Invoice Report
    B. Financial Report
    C. Application Fee Report
    D. Radar Risk Score
    **✔️ Answer: B**

33. **What does a Balance Transaction represent?**
    A. A customer invoice
    B. Bank transfer details
    C. Movement of funds inside your Stripe account
    D. Dispute history
    **✔️ Answer: C**

34. **What report would you use to match payouts to specific charges?**
    A. Refund Summary
    B. Payout Reconciliation Report
    C. Dispute Report
    D. Radar Logs
    **✔️ Answer: B**

---

## ✅ Global Business & Compliance (5% – 3 Questions)

35. **What is required when processing payments internationally?**
    A. Express onboarding
    B. Currency conversion tool
    C. KYC and compliance requirements per region
    D. Only USD pricing
    **✔️ Answer: C**

36. **What’s a reason to configure multiple bank accounts for a business?**
    A. To support faster refunds
    B. For payouts in multiple currencies
    C. For storing refunds separately
    D. To avoid authentication
    **✔️ Answer: B**

37. **How does Stripe help businesses handle currency conversion?**
    A. Through a third-party provider
    B. It automatically converts at competitive rates with a fee
    C. It refuses unsupported currencies
    D. It uses crypto wallets
    **✔️ Answer: B**

---

## ✅ Payment Methods (10% – 5 Questions)

38. **Which payment method is commonly used in Germany and supports deferred payment?**
    A. ACH
    B. Klarna
    C. SEPA
    D. FPX
    **✔️ Answer: B**

39. **Which Stripe feature allows you to send a link to accept payments without coding?**
    A. Checkout Session
    B. Stripe Terminal
    C. Payment Links
    D. API Explorer
    **✔️ Answer: C**

40. **What is the benefit of enabling Payment Method types dynamically on the Payment Element?**
    A. Reduces code complexity
    B. Automatically shows relevant methods per customer location
    C. Adds surcharge fees
    D. Avoids dispute risk
    **✔️ Answer: B**

41. **Which payment method is most suitable for recurring billing in Europe?**
    A. SEPA Direct Debit
    B. Klarna
    C. PayNow
    D. FPX
    **✔️ Answer: A**

42. **How does Stripe help platforms offer localized payment experiences?**
    A. By requiring address verification
    B. Through geo-aware Payment Element rendering
    C. By hiding currencies
    D. By enforcing US card use
    **✔️ Answer: B**

---

## ✅ Radar & Reducing Fraud (10% – 5 Questions)

43. **What powers Radar's fraud detection capabilities?**
    A. Manually written filters
    B. Blockchain analysis
    C. Machine learning trained on global data
    D. Browser cookies
    **✔️ Answer: C**

44. **How does Radar for Fraud Teams enhance fraud prevention?**
    A. Adds machine learning
    B. Gives access to advanced rule creation, insights, and manual review queue
    C. Enables 3D Secure
    D. Charges a higher fee
    **✔️ Answer: B**

45. **What is a common rule example in Radar?**
    A. Block all US cards
    B. Allow all transactions
    C. Block payments from high-risk email domains
    D. Remove SCA
    **✔️ Answer: C**

46. **Which Radar feature scores the likelihood of a payment being fraudulent?**
    A. Smart Retry
    B. Risk Level
    C. Risk Score
    D. Geo Check
    **✔️ Answer: C**

47. **What should a platform do when a payment is flagged with a high Radar risk score?**
    A. Automatically capture
    B. Automatically block or send for manual review
    C. Refund immediately
    D. Send 3DS email
    **✔️ Answer: B**