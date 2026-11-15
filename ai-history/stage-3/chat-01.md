# Stage 3: Happy Hour Feature

**Student:** Amanda Lee

**Group:** 4

**AI tool used:** ChatGPT

### Purpose
Develop the Happy Hour feature for Restaurant Rush.

## **AI Conversation History**
**Amanda:** [Uploaded image of error page from HappyHour.java file] 

**AI Chatbot:** 

You're getting 4 errors in HappyHour.java, but they're mainly caused by two issues:
1. Your Java class declaration has incorrect syntax.
2. VS Code may not be recognising your game package correctly.
---

**Amanda:** Now that happy hour is complete, what are the classes that have to be modified? 

**AI Chatbot:** 

Based on your Stage 2 requirements and your group's Stage 1 architecture, I recommend modifying 5 existing classes, with a possible sixth depending on how your Customer class currently handles satisfaction.
Class	What needs to be added: 
1. GameState.java	Store the Happy Hour instance
2. GameController.java	Allow the manager to activate Happy Hour at the start of a turn
3. TurnProcessor.java	Recover 15 satisfaction at the start of active turns
4. Order.java / ordering logic	Lock the discounted price when the order is taken
5. RestaurantRushCLI.java	Add the activation option and display remaining turns
6. Customer.java	Add a satisfaction recovery method if one doesn't exist

You should not need to modify VIPCustomer.java if it already provides the correct VIP discount behaviour.
The main idea is to let each class perform its existing responsibility rather than putting everything into HappyHour.java.

---

**Amanda:** Why does VIPCustomer.java not need to be modified for Happy Hour?

**AI Chatbot:** 

You do not need to modify this class for Happy Hour. It already handles the VIP discount correctly.
Here's what happens:
1. super.calculateBillCents() calls the method in Customer.java to retrieve the original menu price.
2. originalPrice * 0.90 applies the 10% VIP discount.
3. Math.round() rounds the result to the nearest cent.
4. The method returns the discounted price.

Furthermore because calculateBillCents() in GameController.java is overridden in VIPCustomer, Java automatically calls the VIP version when assigning an order to a VIP customer.

