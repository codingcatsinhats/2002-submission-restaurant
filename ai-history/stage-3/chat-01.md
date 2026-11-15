# SC2002 Restaurant Rush — Stage 3 AI-Assisted Design Discussion

**Student:** Komal Bhandari  
**Group:** 4  
**Stage:** 3  
**Individual Contribution:** Host seating implementation and UML class diagram updates covering Seater, Host, ComboMeal, and HappyHour.
**AI Tool Used:** ChatGPT  
**Documentation:** Selected excerpts from AI-assisted discussions

---

## **AI Conversation History**

**Komal:** for stage 3 do i redraw the whole uml again or just add the new features?

**AI:** Keep a complete Stage 3 class diagram, including the existing Stage 2 classes, and update it to show the new Stage 3 types and relationships. A diagram containing only the new classes would not describe the full system.

**Komal:** so what are the main new things i need to show?

**AI:** Focus on the new `Host`, `Seater`, `HappyHour`, and `ComboMeal` types. Then check the modified classes they interact with, such as `Waiter`, `GameController`, `GameState`, and `Menu`. Use the Stage 3 implementation as the source of truth for attributes, operations, and relationships.

---

**Komal:** host and waiter both seat customers now, so do they inherit from each other?

**AI:** No. They are separate staff classes. Both implement the `Seater` interface, which defines a common seating operation. In UML, use realization relationships (dashed lines with hollow triangles) pointing from `Host` and `Waiter` toward `Seater`.

**Komal:** why use an interface instead of just putting the same seat method in both?

**AI:** An interface makes the shared capability explicit. Code can reason about the `Seater` contract without treating `Host` as a kind of `Waiter`, or vice versa. It also avoids implying an incorrect inheritance hierarchy. Whether the rest of the code fully depends on that abstraction should be checked against the implementation rather than assumed.

**Komal:** is that dependency inversion then?

**AI:** It supports interface-based design and the idea behind the Dependency Inversion Principle, but be precise: simply declaring an interface does not prove that every higher-level component depends only on abstractions. In your explanation, point to the actual `Seater` relationship and avoid overstating the extent of decoupling.

---

**Komal:** where should happy hour go in the uml? is it a customer subclass?

**AI:** No. `HappyHour` represents a game promotion, not a customer type. Show it in the game area and use the relationship actually present in the Stage 3 code and UML source to connect it with the relevant game state or controller. Do not make it inherit from `Customer`.

**Komal:** and combo meal extends menu item right?

**AI:** Yes, `ComboMeal` extends `MenuItem`. Show the generalization arrow pointing to `MenuItem`. A combo can therefore be treated as a menu item while introducing its own behaviour. Check the implementation before adding specific fields or pricing methods to the diagram.

**Komal:** so is combo meal inheritance or composition?

**AI:** It can involve both, but in different ways: `ComboMeal` **inherits from** `MenuItem`, and it may **contain or refer to** component dishes. Only draw a composition or association to those dishes if the code supports that precise relationship. Do not use a composition diamond just because the word “combo” suggests parts.

---

**Komal:** i want the stage 3 uml to look organised, but it has so many classes now.

**AI:** Group classes by their existing packages and make the new relationships easy to follow. For example, focus the staff section on `Host`, `Waiter`, and `Seater`, the game section on `HappyHour`, and the menu section on `ComboMeal` and `MenuItem`. Keep the full Stage 3 system visible, rather than deleting older classes to make space.

**Komal:** how do i make sure my diagram is actually correct?

**AI:** Compare the diagram with the Stage 3 Java source file by file. Verify class and interface names, method signatures, inheritance and implementation arrows, and associations. If the rendered PNG looks different from the `.puml` source, inspect both; the source alone does not prove what is visible in the submitted image.

---

**Komal:** for the video i need to explain how the design changed from stage 2 to stage 3\. what should i focus on?

**AI:** Show the GitHub `stage-2...stage-3` comparison and explain the four new production Java types: `Host`, `Seater`, `HappyHour`, and `ComboMeal`. Then connect those additions to the UML relationships. Distinguish added and modified production source files from tests, diagrams, and documentation in GitHub's overall changed-file count.

**Komal:** and how do i connect it to solid without just saying all the principles?

**AI:** Use concrete examples. `Seater` defines a common contract for different seating roles; `ComboMeal` extends the existing `MenuItem` abstraction; and the promotion functionality is represented separately rather than being described as a new customer subtype. Explain what each decision helps with, and only claim principles that the code actually demonstrates.

**Komal:** so the main takeaway is we added features without rewriting everything?

**AI:** Yes, but phrase it carefully: Stage 3 still required modifications to existing files. The point is that the earlier object-oriented structure gave the team reusable classes and abstractions, so new features could be integrated through targeted changes rather than a complete redesign.

---

**Komal:** can i use these explanations directly in my uml and video?

**AI:** Use them as a guide, but check the final diagram and implementation yourself. Your submitted UML should reflect the code, and your narration should describe what the repository actually contains. The AI discussion supports your understanding; it does not replace verification or your group's design decisions.