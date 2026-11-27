# Activity 3: "Procedural vs. Event-Driven" - Side-by-Side Coding

Code: [`procedural/ProceduralCalculator.java`](procedural/ProceduralCalculator.java) and [`eventdriven/EventDrivenCalculator.java`](eventdriven/EventDrivenCalculator.java)

## Procedural Calculator - Notes

1. **Exact order of steps:** (1) ask for the first number, (2) ask for the operator, (3) ask for the second number, (4) calculate with a `switch`, (5) display the result, then the program ends.
2. **Wrong input at step 2:** If the user types something that is not `+ - * /`, the `default` case prints "Invalid operator" and the program ends. The user has to restart. (If a non-number is typed at step 1 or 3, `nextDouble()` throws an `InputMismatchException` and the program crashes.)
3. **Calculate again without restarting?** No. The program runs once from top to bottom and exits.
4. **Who controls the flow?** The program. It decides what is asked and in what order; the user can only answer when prompted.

## Event-Driven Calculator - Notes

1. **Click buttons in any order?** Yes. Any button can be clicked at any time and the matching handler runs.
2. **If the user makes a mistake?** They can press **C** to clear and start again, or just keep entering numbers. Nothing crashes the whole program (e.g. dividing by zero shows "Error"). One weakness: pressing an operator or `=` while the display says "Error" throws a `NumberFormatException` in the handler (printed to the console), but the window keeps running.
3. **Calculate again without restarting?** Yes. After `=`, the user can enter new numbers immediately or press **C**.
4. **Who controls the flow?** The user. The program just waits and reacts to events.
5. **How many event handlers?** There are **4 handler definitions**: number buttons, operator buttons, equals, and clear. Because the number handler is registered on 10 buttons and the operator handler on 4 buttons, the program has **16 `ActionListener` registrations** in total (10 + 4 + 1 + 1).

## Comparison Table

| ASPECT | PROCEDURAL | EVENT-DRIVEN |
|---|---|---|
| Who controls the flow? | The program (fixed sequence of steps) | The user (program reacts to their actions) |
| Can user make mistakes and recover easily? | No. A mistake usually ends the program or crashes it, and the user must restart | Yes. The user can press Clear or enter a new value and continue |
| Can user interact in any order? | No. Must follow the order of prompts | Yes. Any button/control at any time |
| How many possible execution paths? | Few. One main path with a small number of branches | Many. Depends on the sequence of events the user chooses |
| Code organization | One main method written top to bottom | Many small handlers (one per event), plus shared state |
| User experience | Rigid, text-based, one calculation per run | Interactive, flexible, visual, reusable |

## Reflection

The main difference is who is in control: a procedural program follows a fixed sequence that the programmer decided, while an event-driven program waits for events and reacts to whatever the user does. In the procedural calculator the user could only answer prompts in order and had to restart for every calculation, whereas the event-driven calculator let me click any button at any time and keep calculating. For interactive applications I prefer the event-driven approach because it is more natural and forgiving for users. Event-driven programming suits GUIs because users can click, type or resize in unpredictable orders, and handlers let each action be dealt with separately. It also keeps the code organized into small pieces, each responsible for one event. Procedural programming is still useful for simple scripts and batch tasks with a clear start-to-finish flow.
