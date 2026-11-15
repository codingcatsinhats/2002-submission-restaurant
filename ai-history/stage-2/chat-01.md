# Stage 2: UML Sequence Diagram for Critic 

**Student:** Amanda Lee

**Group:** 4

**AI tool used:** ChatGPT

### Purpose
Develop UML Sequence diagram showing Critic feature, including one manager decision that could affect the outcome of the game 

## **AI Conversation History**
**Amanda:** why isGameOver() added in turn 13 

**AI chatbot:** isGameOver() appears on Turn 13 because your actual RestaurantCLI.run() uses a while loop, this means isGameOver() is checked before every turn, not just Turn 13.

--- 
**Amanda:** The loop only mentions reducing customer's satisfaction, so since from turn 13-> 16, the critic loses satisfaction thrice (end of turn 13, 14, 15)? 

**AI chatbot:** 
Yes, exactly correct! The Critic loses satisfaction three times before Turn 16 begins, because updateSatisfaction() is called at the end of every turn. 
When the Waiter serves the Critic on Turn 16, onServed(16) changes the Critic's status to EATING.
Therefore, even though updateSatisfaction() still calls decreaseSatisfaction() at the end of Turn 16, nothing is deducted because the Critic is no longer WAITING or SEATED.

--- 
**Amanda:** Why is decreaseSatisfaction() called even though customer's satisfaction remains constant?

**AI chatbot:**
Because calling decreaseSatisfaction() does not necessarily mean satisfaction decreases. There are two separate things happening in your Java code.

1. TurnProcessor.java calls the method for every customer
2. CriticCustomer.java decides whether to deduct satisfaction

Your existing diagram is technically correct, but it can be misleading because it doesn't show the condition inside decreaseSatisfaction()




