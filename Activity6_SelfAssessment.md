# Activity 6: Final Self-Assessment

## Learning Outcome 1: Define EDP Components

1. **What is an event? Give two examples.** An event is a signal that something has happened in the system, usually represented as an object. Examples: a mouse click, a key press (also a timer firing, a file being changed).
2. **What is an event source? Give two examples.** The object or device that generates the event. Examples: a `JButton`, a keyboard (also a sensor, a timer, a network socket).
3. **What is an event listener? Give two examples.** An object registered with a source that waits for and receives its events. Examples: an `ActionListener` on a button, a `KeyListener` on a text field (also a `MouseListener`).
4. **What is an event handler? Give two examples.** The code that runs in response to an event. Examples: the `actionPerformed` body that adds a digit to the calculator display; a method that shows an alarm message when a door sensor triggers.
5. **Diagram:**

```
 Event Source  ──generates──►  Event  ──delivered to──►  Event Listener  ──invokes──►  Event Handler
   (JButton)               (ActionEvent)               (ActionListener)           (actionPerformed code)
        ▲                                                                                  │
        └────────────────── listener is registered with the source ◄──────────────────────┘
                              (addActionListener)                      handler updates the GUI/state
```

## Learning Outcome 2: Compare Paradigms

6. **Procedural vs event-driven:** Procedural programs run a predetermined sequence of steps from start to finish, so the program controls the flow. Event-driven programs wait for events and run handlers in response, so the flow is controlled by external events such as user actions.
7. **Main advantage for GUIs:** Users can interact with any control in any order at any time, and the application stays responsive, with each action handled separately.
8. **When to choose procedural:** For simple, linear tasks with a clear start and end and no interaction, e.g. a script that converts a file, a batch data-processing job, or a one-off calculation.

## Learning Outcome 3: Event Loop and Queue

9. **Event loop:** A loop that continually checks the event queue, takes the next event, and runs the handler associated with it, then repeats.
10. **Event queue:** A first-in, first-out list where events wait until the event loop is ready. New events are added to the back and the loop removes them from the front.
11. **Why never block it?** Handlers run one at a time. If one takes too long, all other events wait, so the application freezes and cannot repaint or respond.
12. **EDT:** The Event Dispatch Thread is the single thread in Java Swing that runs the event loop, executes event handlers, and updates Swing components.

## Learning Outcome 4: Real-World Examples

13. **Five real-world event-driven systems:** ATM, elevator, traffic light controller, video game, smartphone touchscreen (also microwave oven, alarm systems).
14. **All four components for one system (Elevator):**
    - *Event source:* the floor call button
    - *Event:* button pressed
    - *Listener:* the elevator controller
    - *Handler:* add the floor to the request queue, light up the button, move the elevator
15. **Why are modern applications event-driven?** Because they must respond to many unpredictable inputs (clicks, touches, messages, network data, sensors) while staying responsive. Event-driven design lets them react only when something happens, handle things in any order, and keep code modular.

## Score

Self-score (13-15 excellent, 10-12 good, 7-9 satisfactory, below 7 needs improvement): **____ / 15**
*(Check your own answers against the activities and fill this in yourself.)*

---

# One-Page Summary: Week 1 - Event-Driven Programming

**Key definitions**
- **Event** - a signal that something happened (click, key press, timer, sensor reading).
- **Event source** - what generates the event (button, sensor, timer).
- **Event listener** - registered object that waits for events from a source.
- **Event handler** - the code that runs in response.
- **Event queue** - FIFO line of pending events. **Event loop** - repeatedly takes the next event from the queue and runs its handler.
- **EDT** - the single Event Dispatch Thread in Swing that runs the loop and owns the GUI.

**Important diagram**
```
Source ─► Event ─► Event Queue ─► Event Loop (EDT) ─► Listener ─► Handler ─► GUI update
```

**Procedural vs event-driven**
Procedural: program controls the flow, fixed order, one run. Event-driven: user/events control the flow, any order, continuous waiting. Event-driven is better for GUIs and interactive systems.

**Rules I learned (from the bug-fix activity)**
1. Never block the EDT. Run long tasks in a background thread (Bug 1).
2. A component with no listener does nothing, so always register the listener (Bug 2).
3. Only touch Swing components from the EDT, using `SwingUtilities.invokeLater()` (Bug 3).
4. Remove references (e.g. clear lists) when removing components, so they can be garbage collected (Bug 4).

**Code example I found helpful**
```java
button.addActionListener(e -> {
    new Thread(() -> {
        doLongTask();                                   // background thread
        SwingUtilities.invokeLater(() -> label.setText("Done!")); // back on the EDT
    }).start();
});
```

**Questions I still have**
- When should I use `SwingWorker` instead of `Thread` + `invokeLater`?
- How does the Observer Pattern (Week 2) relate to listeners and sources?
- How do event loops in other environments (e.g. JavaScript/Node.js) compare to the Swing EDT?
