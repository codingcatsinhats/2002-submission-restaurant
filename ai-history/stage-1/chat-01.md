# SC2002 Restaurant Rush — Stage 1 AI-Assisted Design Discussion

**Student:** Komal Bhandari  
**Group:** 4  
**Stage:** 1  
**Individual Contribution:** Menu implementation, testing, and UML class diagram.  
**AI Tool Used:** ChatGPT  
**Documentation:** Selected excerpts from AI-assisted discussions

---

## **AI Conversation History**

**Komal:** for my menu part, should `Menu` store the items or should `MenuItem` manage the list?

**AI:** `MenuItem` should represent one dish, with properties such as name, price and preparation units. `Menu` should hold and expose the collection of available dishes. That separates the responsibility for a single item from the responsibility for the overall menu.

**Komal:** so for our salad burger pasta, the prep time belongs in each item right? pasta needs 2 units while the other two need 1

**AI:** Yes. The chef can read the chosen item's preparation units from the order instead of hard-coding dish names into the chef logic. For Stage 1, Salad is \$9/1 unit, Burger \$15/1 unit, and Pasta \$18/2 units.

**Komal:** but why not just make the item fields public? less getters

**AI:** Keeping fields private supports encapsulation. Other classes can read information through getters without being able to change a dish's price or preparation units unexpectedly.

---

**Komal:** what tests should i write for menu? i already checked that the 3 items exist

**AI:** In addition to checking that the three expected items are present, verify each item's price and preparation units, and any lookup or validation behaviour actually exposed by your `Menu` implementation. Don't write tests for methods that don't exist in the Stage 1 code.

**Komal:** so checking just the size 3 isn't enough?

**AI:** Right. A menu could have three items but still have the wrong prices or preparation units. Assertions about the actual item properties catch those mistakes.

**Komal:** okay then the tests should match the requirements and not just pass because the list has 3 things

**AI:** Exactly. A useful test checks the intended behaviour, not just that some code ran.

---

**Komal:** i'm confused why we have both `GameController` and `TurnProcessor`. can't controller do everything?

**AI:** It could technically, but separating responsibilities makes the code easier to follow. `GameController` coordinates the current turn and player actions; `TurnProcessor` handles end-of-turn processing. `GameState` stores the shared state. That also helps avoid one oversized class.

**Komal:** then should customer arrivals be in the end of turn processor too?

**AI:** Not automatically. Follow the sequence in your Stage 1 implementation and requirements. Arrivals occur on turns 1, 4, 7, 10, 13 and 16, so the timing matters. Place the logic according to the agreed flow rather than moving it solely because the class is named `TurnProcessor`.

**Komal:** okay so UML must follow actual code not just what sounds like better design

**AI:** Correct. A class diagram for the implemented Stage 1 should describe the tagged Java source, even if you can imagine a different architecture.

---

**Komal:** when i draw the class diagram do i need to put every private helper method? it's getting so messy

**AI:** For a readable implementation diagram, show the key fields, constructors and public/protected operations. You can omit private helpers if you state that convention. Keep class names, inheritance and important relationships accurate.

**Komal:** and if the final CLI changed after i made the diagram?

**AI:** Recheck the diagram against the final `stage-1` tag, not an earlier branch. The final CLI may contain additional constants or nested classes. The diagram should reflect the submitted version.

**Komal:** wait the `WaitChoice`, `SeatChoice`, `TakeOrderChoice`, `ServeChoice` classes should point to `WaiterChoice` with inheritance right?

**AI:** Yes. Those concrete choice classes extend the abstract `WaiterChoice` class, so UML generalisation arrows should point toward `WaiterChoice`. The `WaiterAction` enum is a separate type used to represent the action.

**Komal:** and don't add stage 2 classes even if teammates already started working on them

**AI:** Exactly. Stage 1's diagram should represent Stage 1 only. Use the `stage-1` snapshot as the boundary.