# Introducing Payment Processing System

Created: September 15, 2022 2:09 PM
Created by: Tymur Yarosh
Modified: March 15, 2023 11:44 PM

**The problem**

Around 2000 BCE, prototype banks gave loans to the first farmers and traders. The loan was the very first and the only bank service. Later, the family of services increased by deposits and the change of money operations. These days banks are much more complex businesses. They provide money transfer services, mortgages, card payments, and many more. All services end up in a payment transaction. The transaction processing procedure consists of numerous different steps. For instance, money transfer between clients of the same bank from the business perspective can consist of:

1. Verifying if the operation invoked by the authorized party
2. Verifying if the debtor account is eligible for withdrawing
3. Verifying if the debtor account has enough money to cover the transaction
4. Verifying if the creditor account is eligible for receiving
5. Verifying the transaction for fraud
6. Changing the balance of the debtor account (the sending party)
7. Changing the balance of the creditor account (the receiving party)

The process is more complex from a technical perspective — countless calls between multiple software systems. While implementing the procedure, developers consider authorizations, retries, idempotency, rollbacks, and many others common for distributed systems.

Governments make the process even more difficult by regulating the industry and forcing banks to inject additional reporting and verification steps into the established procedure.

Banks create new types of transactions when introducing new services. They change a transaction to comply with internal changes of the enterprise or follow new regulations. After all, banks change particular steps to adjust low-level details such as credentials or API calls.

Therefore, today’s banks require a sophisticated solution to:

- Make transaction processing procedure easy to change
- Introduce new transaction processing procedures as easy as possible
- Decouple transaction processing from the application business rules

**The solution**

![Architecture - C1.png](Introducing%20Payment%20Processing%20System%20769f17b409b64c9db1c77663d10c8a67/Architecture_-_C1.png)

This is where the payment processing system (PPS) brings its value. PPS is an engine and a framework to process payment transactions. The engine orchestrates transaction processing steps. It’s responsible for step invocation, retrying attempts in case of step failure, and rolling back the whole transaction. The framework enables software developers to implement transaction processing steps and compose them into a processing procedure called “Flow.”

The PPS engine provides HTTPS API to post payment transactions or get transaction details. The API is intended for private usage inside the enterprise. Bank software that needs transaction processing capabilities invokes the PPS engine’s API to process the transaction.

Readers familiar with Open Banking can consider the following example: PPS runs behind the Account Servicing Payment Service Provider (ASPSP) API. Payment Initiation Services Provider (PISP) negotiates payment consent and payment order with ASPSP API, and ASPSP sends the payment order to PPS for asynchronous processing.
