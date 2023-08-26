## FeedMe Security Engineer Take-Home Assignment
Below is a take-home assignment before the interview for the position. You are required to
1. Understand the requirement, you may contact the interviewer for further clarification.
2. You can complete your task with any tool you familiar with.
3. Document your finding in English.
4. Bring your result to the next interview session.

### Situation
As FeedMe merchant are growing fast, our feature request are also increasing. One of the favourite feature is membership topup, because our merchant can secure the money and guarantee the user will come back later. As secuirty engineer in FeedMe, your task is to work together with product owner and identify and design the security requirement for this feature.

### Requirement
Below is the initial system requirement that being designed
- 01: Merchant who enable topup feature will get their topup page `http://member.feedme.cc/<merchant-code>`
- 02: Each customer is identify by their mobile phone number
- 03: Customer able to choose their topup package (eg: RM10, RM20, RM50)
- 04: Customer will key in the their credit card number for payment and the system will remember the card inside the database
- 05: The system then will charge the card with the desire amount and increase the customer balance
- 06: Customer able to check and consume their balance by visitng the outlet
- 07: When customer want to consume their credit, they will provide their phone number to cashier, then cashier will deduct the bill total from their balance through and API call and return a receipt

### Result
With above system requirement, you as a security are required to identify and design the security requirement for our software engineer to ensure the whole topup system are protected from any vulnerability. Your requirement should consist the following criteria:
- readable for various audiences, eg: product team, engineering team
- reference that support your requirement and design
- design should be implementable with example
Example:
Requirement 01: The page route should use `https` instead of `http` as suggested in by cloudflare (https://www.cloudflare.com/learning/ssl/why-use-https/). For example cloudflare specify the encryption mode when connecting to the server (https://developers.cloudflare.com/ssl/origin-configuration/ssl-modes/)

### Tips on completing this assignment
- Try to scope your working hour within 3 hours (1 hour per day if you are really busy) and avoid unnecessary optimization and documentation.
- Communicate effectively like you are going to communicate with the actual team member.
