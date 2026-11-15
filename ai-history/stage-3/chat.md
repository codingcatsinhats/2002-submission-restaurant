# Stage 3 AI Chat History — Alexa (Person 2)
**Module Scope:** Stage 2 -> 3 Integration Check & Report Phrasing (`Customer`, `VIPCustomer`, `CustomerChoiceGenerator`, `Order`)

---

### Exchange 1: Verifying Compatibility with Stage 3 `ComboMeal` and `HappyHour`
**User:**
In Stage 3, `CustomerChoiceGenerator` assigns `menu.getComboMeal()` to customer C4 (`COMBO_CUSTOMER_ID = 4`), and Happy Hour applies promotional adjustments in `GameController` alongside `Customer.increaseSatisfaction(int amount)`. Do `VIPCustomer` or `CriticCustomer` need any modifications?

**Assistant:**
No changes are needed in `VIPCustomer` or `CriticCustomer`:

1. **Combo Meal Billing:** Because `ComboMeal` extends `MenuItem`, `Customer.calculateBillCents()` reads the item price in cents, `VIPCustomer` applies its 10% discount, and `Customer.assignOrder(Order)` locks that amount into `Order` via `setFinalPriceCents()`. `GameController` then applies Happy Hour pricing afterwards on top of `order.getFinalPriceCents()`.
2. **Happy Hour Satisfaction Boost:** Because `increaseSatisfaction(int amount)` is defined on `Customer` and bounded by `MAX_SATISFACTION` (`100`), both `VIPCustomer` and `CriticCustomer` inherit satisfaction recovery cleanly without affecting their overridden `decreaseSatisfaction()` decay constants (`5` and `12`).

---

### Exchange 2: Wording Check for Report Sections
**User:**
Can you check the clarity and phrasing of my draft paragraph for the `Trade-offs` section comparing class inheritance against the Strategy pattern?

**Draft:**
> Customer differences through the use of inheritance (`VIPCustomer`, `CriticCustomer`) compared to strategy objects (`DecayStrategy`, `DiscountStrategy`) on one `Customer` class were considered. While Strategy pattern offers runtime behaviour swapping, customer types in Restaurant Rush are fixed upon arrival. The use of class inheritance is simpler in terms of object creation, ensuring type safety at compile time, and accurately reflecting the real-world domain.

**Assistant:**
Your points are clear and accurate. To tighten the phrasing slightly:

> Representing customer variations via inheritance (`VIPCustomer`, `CriticCustomer`) was weighed against attaching strategy objects (`DecayStrategy`, `DiscountStrategy`) to a single `Customer` class. While the Strategy pattern supports runtime behavior swapping, customer types in *Restaurant Rush* are fixed upon arrival. Class inheritance was selected because it simplifies object instantiation, enforces compile-time type safety, and directly mirrors the domain hierarchy.