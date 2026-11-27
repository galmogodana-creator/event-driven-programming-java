# Event-Driven System Design

## System Name: Parking Garage

---

## Part 1: Event Sources

List all components that can generate events:

1. **Entry gate sensor** - generates "Car Arrived" events when a vehicle triggers the entry loop sensor
2. **Payment machine** - generates "Ticket Paid" events when a driver pays (card/cash)
3. **Exit gate sensor** - generates "Car At Exit" events when a vehicle reaches the exit barrier
4. **Operator control panel** - generates "Garage Reset" events (and manual overrides)
5. **System timer/clock** - generates "Timer Tick" events (e.g. every second) to update the clock and calculate parking duration

---

## Part 2: Events

List all possible events in the system:

| Event Name | Source | Description |
|---|---|---|
| CarArrived | Entry gate sensor | A vehicle is detected at the entry gate |
| TicketPaid | Payment machine | A driver successfully pays the parking fee |
| CarAtExit | Exit gate sensor | A vehicle is detected at the exit barrier |
| GarageReset | Operator control panel | The operator clears the counters/log (start of day) |
| TimerTick | System timer | One second has passed; refresh clock/duration |

---

## Part 3: Event Handlers

For each event, describe what should happen:

| Event | Handler Action |
|---|---|
| CarArrived | If a space is free: issue a ticket, open the barrier, increment cars inside, update free spaces. If full: keep the barrier closed and show "FULL". |
| TicketPaid | Mark one ticket as paid, add the fee to revenue, allow the car to exit, log the payment. If there are no unpaid cars, ignore and log it. |
| CarAtExit | If the ticket is paid: open the barrier, decrement cars inside, free the space. If unpaid: keep the barrier closed and prompt for payment. If the garage is empty: log an anomaly. |
| GarageReset | Set counters and revenue to zero, clear the event log, show "System Ready". |
| TimerTick | Update the clock label on the display. |

---

## Part 4: Event Flow Diagram

```
 Entry sensor ─┐
 Payment mach. ─┤
 Exit sensor  ──┼─→ Event Object ─→ Event Queue ─→ Event Loop (EDT) ─→ Listener ─→ Handler ─→ State + GUI update
 Operator panel ┤                    (FIFO)         (takes next event)                          (cars, revenue,
 Timer ─────────┘                                                                                log, barrier)
```

Example: *Driver presses "Pay Ticket"*

```
Payment button ─→ ActionEvent ─→ Event Queue ─→ EDT picks it up ─→ payButton ActionListener
              ─→ handlePayment() ─→ carsPaid++, revenue += fee ─→ refreshDisplay() + logEvent()
```

---

## Part 5: Potential Issues

What could go wrong with this system?

1. **Slow handler blocks the event loop** (e.g. a payment handler that waits on a bank server freezes the entry/exit display) - *Prevent it by running network/payment calls in a background thread and updating the GUI with `SwingUtilities.invokeLater()`.*
2. **Race conditions on shared state** (entry, exit and payment events changing `carsInside` at the same time) - *Prevent it by handling all state changes on the single EDT, or by using synchronized/atomic counters if background threads are involved.*
3. **Car leaves without paying / sensor misfires** (a stuck sensor sends duplicate "Car Arrived" events) - *Prevent it by validating state in every handler (check for full/empty/unpaid), debouncing sensor events, and logging anomalies.*
