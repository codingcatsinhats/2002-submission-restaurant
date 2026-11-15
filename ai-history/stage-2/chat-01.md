# SC2002 Restaurant Rush — Stage 2 AI-Assisted Design Discussion

**Student:** Komal Bhandari  
**Group:** 4  
**Stage:** 2  
**Individual Contribution:** UML class diagram updates for Stage 2 customer inheritance, polymorphism, and pricing changes.
**AI Tool Used:** ChatGPT  
**Documentation:** Selected excerpts from AI-assisted discussions

---

## **AI Conversation History**

**Komal:** for stage 2 uml do i redraw everything from stage 1 or just add the new customer types?

**AI:** Keep the Stage 1 structure and update the classes, operations and relationships that changed. The Stage 2 diagram should still show the complete system, not just the two new classes.

**Komal:** VIPCustomer and CriticCustomer both extend Customer right? so two arrows pointing to Customer?

**AI:** Yes. Both have separate UML generalisation arrows pointing to `Customer`. They do not inherit from each other.

**Komal:** since Customer already stores satisfaction do i need to add satisfaction again under both subclasses?

**AI:** No. The subclasses inherit the existing satisfaction state. Show their overridden satisfaction behaviour instead of duplicating the attribute.

---

**Komal:** their satisfaction goes down at different rates though, how should i show that without making the diagram too crowded?

**AI:** Show the relevant `decreaseSatisfaction()` overrides and, if useful, a short note: regular customers lose 8 points, VIP customers 5, and Critic customers 12 per applicable turn. Keep the notes separate from the method signatures.

**Komal:** okay and the VIP 10% discount, does that mean i change Cashier in the diagram?

**AI:** Not just because a VIP discount exists. The customer-specific bill calculation is represented by the overridden `calculateBillCents()` method in `VIPCustomer`. Check the actual Stage 2 code before changing any `Cashier` operation.

**Komal:** so for Critic preferring pasta is that `chooseMenuItem()` being overridden?

**AI:** Yes, if that's how the implemented code expresses the preference. Show the override in `CriticCustomer` and retain the common operation in `Customer`.

---

**Komal:** should CustomerChoiceGenerator point to VIPCustomer and CriticCustomer separately then?

**AI:** If it calls methods through the `Customer` parent type, a relationship to `Customer` is enough. Polymorphism lets the concrete customer type determine the behaviour at runtime.

**Komal:** but if i only draw Customer will it look like i forgot the new classes?

**AI:** Not if the inheritance relationships are shown clearly. The subclasses appear in the diagram, while the generator's dependency remains on the shared parent type.

**Komal:** i saw finalPriceCents in Order. should that be included even though my main change is the customer classes?

**AI:** Yes. The UML should reflect relevant Stage 2 implementation changes beyond inheritance. Include the price field and any corresponding operation, such as `setFinalPriceCents()`, if they exist in the tagged code.

---

**Komal:** GameController also creates the different customer types for specific arrival turns. do i list all the turns in the class box?

**AI:** No need to put the full arrival schedule inside a class box. Show the relevant controller operations and relationships. You can explain the scheduled arrivals in the report text if needed.

**Komal:** so GameController still handles them as Customer after creating the subclass?

**AI:** Yes. The controller can hold and process them through `Customer` references, while the overridden methods supply type-specific behaviour.

**Komal:** is it okay if the UML doesn't show every private helper? it gets too small in the report

**AI:** Use the same readability convention as Stage 1: show the important attributes, constructors and operations, and omit nonessential private helpers consistently. Don't omit key inheritance or relationships.

**Komal:** okay i'll compare the final diagram to the stage 2 code instead of just copying the stage 1 one and guessing

**AI:** That's the right check. Verify names, visibility, signatures, inheritance and dependencies against the completed Stage 2 snapshot, and avoid including Stage 3 features prematurely.