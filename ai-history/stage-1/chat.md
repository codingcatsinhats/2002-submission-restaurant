# Stage 1 AI Chat History — Alexa (Person 2)
**Module Scope:** `Customer`, `CustomerStatus`, `Order`, `OrderStatus`, `CustomerChoiceGenerator`

---

### Exchange 1: Encapsulating Customer Lifecycle Transitions
**User:**
For Stage 1 `Customer.java`, is it better to expose a public `setStatus(CustomerStatus status)` setter or handle state changes through specific methods like `seatAt()`, `onServed()`, `finishEating()`, `onPaid()`, and `leave()`?

**Assistant:**
Encapsulating state changes inside dedicated domain methods (`seatAt()`, `onServed()`, `finishEating()`, `onPaid()`, and `leave()`) is cleaner and safer than relying on a public setter:

1. **Precondition Validation:** `seatAt(Table table)` verifies that `status == CustomerStatus.WAITING` and `table != null && table.isAvailable()` before transitioning to `SEATED` and calling `table.occupy(this)`.
2. **Atomic Cleanup on Abandonment:** `leave()` sets `status = CustomerStatus.LEFT`, releases the occupied table (`table.free()`), and cancels any unpaid order (`order.cancel()`) in one place.
3. **Invariant Enforcement:** Keeping `satisfaction` updates inside `decreaseSatisfaction()` (`Math.max(0, satisfaction - DEFAULT_SATISFACTION_LOSS_PER_TURN)`) ensures satisfaction stays bounded between `0` and `MAX_SATISFACTION` (`100`).

---

### Exchange 2: Tracking Order Preparation Units and Serving Eligibility
**User:**
In `Order.java`, orders that become `READY` on turn $t$ can only be served starting on turn $t + 1$. How should `advance(int currentTurn)` and serving validation track this?

**Assistant:**
Store `readyTurn = -1` and record `currentTurn` when `remainingUnits` reaches `0`, then expose a helper `canBeServedOn(int turn)`:

    public boolean canBeServedOn(int turn) {
        return status == OrderStatus.READY && turn > readyTurn;
    }

    public void advance(int currentTurn) {
        if (status == OrderStatus.PLACED) {
            status = OrderStatus.PREPARING;
        }
        if (remainingUnits > 0) {
            remainingUnits--;
        }
        if (remainingUnits == 0 && status != OrderStatus.READY) {
            status = OrderStatus.READY;
            readyTurn = currentTurn;
        }
    }

Similarly, in `Customer.java`, `canPayOn(int currentTurn)` checks `status == CustomerStatus.READY_TO_PAY && currentTurn > readyToPayTurn` so payment happens on the turn after eating finishes.

---

### Exchange 3: Deterministic Menu Selection in `CustomerChoiceGenerator`
**User:**
Can you double-check my deterministic selection formula `(customerId - 1) % items.size()` in `CustomerChoiceGenerator.chooseItem(Menu menu, Customer customer)`?

**Assistant:**
Using `Math.abs(customer.getCustomerId() - 1) % items.size()` deterministically cycles through the menu (`C1` -> index `0`, `C2` -> index `1`, `C3` -> index `2`, wrapping around). Be sure to check `if (items == null || items.isEmpty())` first and throw `IllegalStateException` so an empty menu never triggers a divide-by-zero error.