# Stage 2 AI Chat History — Alexa (Person 2)
**Module Scope:** `Customer`, `VIPCustomer`, `CriticCustomer`

---

### Exchange 1: Inheritance vs. Strategy Pattern for Stage 2 Customer Types
**User:**
In Stage 2 we need `VIPCustomer` (5 satisfaction loss/turn, 10% bill discount) and `CriticCustomer` (12 satisfaction loss/turn, always orders Pasta). Should I make them subclasses of `Customer` or pass strategy objects into `Customer`?

**Assistant:**
Using class inheritance (`VIPCustomer extends Customer` and `CriticCustomer extends Customer`) is the better design here:

* **Fixed Customer Type:** A customer's archetype is fixed upon arrival in `GameController`, so runtime strategy swapping is not needed.
* **Polymorphic Dispatch Without `instanceof`:** `TurnProcessor`, `Cashier`, and `RestaurantCLI` can hold `Customer` references and call `decreaseSatisfaction()`, `calculateBillCents()`, `chooseMenuItem()`, and `getCustomerTypeLabel()` dynamically without `if/else` or `instanceof` checks.
* **Shared State Machine:** Both subclasses inherit `seatAt()`, `assignOrder()`, `onServed()`, `finishEating()`, `onPaid()`, and `leave()` without duplicating lifecycle fields.

---

### Exchange 2: Implementing `VIPCustomer` Discount Rounding and `CriticCustomer` Menu Override
**User:**
How should `VIPCustomer.calculateBillCents()` apply the 10% discount in integer cents, and how should `CriticCustomer` enforce always ordering Pasta?

**Assistant:**
1. **`VIPCustomer.calculateBillCents()`:** Delegate to `super.calculateBillCents()` and use half-up integer rounding with `VIP_DISCOUNT_PERCENT = 10`:

    @Override
    public int calculateBillCents() {
        int originalPrice = super.calculateBillCents();
        return (originalPrice * (100 - VIP_DISCOUNT_PERCENT) + 50) / 100;
    }

2. **`CriticCustomer.chooseMenuItem(List<MenuItem> items)`:** Override `chooseMenuItem` on `Customer` so `CriticCustomer` searches `items` for `"Pasta"` (falling back to `super.chooseMenuItem(items)` if absent), while `VIPCustomer` inherits the default index rotation from `Customer`.