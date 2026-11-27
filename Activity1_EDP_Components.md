# Activity 1: "Spot the Components" - Real-World EDP Scavenger Hunt

## Components Table

| # | System | Event Source | Event | Listener | Handler/Action |
|---|--------|--------------|-------|----------|----------------|
| 1 | ATM Machine | Keypad button | Button pressed | ATM software | Verify PIN |
| 2 | ATM Machine | Card slot | Card inserted | Card reader | Read card data |
| 3 | ATM Machine | Cash dispenser | Cash taken | Sensor | End transaction |
| 4 | Microwave Oven | Door sensor | Door opened | Safety interlock circuit | Stop heating, turn on light |
| 5 | Microwave Oven | Start button | Start pressed | Control board | Begin heating, start countdown |
| 6 | Microwave Oven | Internal timer | Time reached 0 | Control board | Stop magnetron, beep |
| 7 | Traffic Light | Vehicle sensor (road loop) | Vehicle detected | Traffic controller | Request green phase for that road |
| 8 | Traffic Light | Pedestrian button | Button pressed | Traffic controller | Queue pedestrian crossing, show WALK signal |
| 9 | Traffic Light | Phase timer | Timer expired | Traffic controller | Switch to next light colour |
| 10 | Video Game | Gamepad / keyboard | Button pressed | Game input system | Move character / jump / shoot |
| 11 | Video Game | Collision detector | Player hits enemy | Game engine | Reduce health, play sound |
| 12 | Video Game | Game timer | Level time expired | Game engine | Show "Game Over" screen |
| 13 | Elevator | Floor call button | Button pressed | Elevator controller | Add floor to queue, light up the button |
| 14 | Elevator | Door sensor | Beam interrupted | Door controller | Re-open doors |
| 15 | Elevator | Floor sensor | Reached target floor | Elevator controller | Stop motor, open doors |
| 16 | Smartphone touchscreen | Touch panel | Tap / swipe | Operating system (touch driver) | Open app / scroll the screen |
| 17 | Online shopping website | "Add to cart" button | Button clicked | JavaScript click listener | Add item to cart, update cart count |
| 18 | Security alarm system | Motion detector | Motion detected | Alarm control panel | Sound siren, notify owner |
| 19 | Self-checkout | Barcode scanner | Item scanned | Checkout software | Add item and price to the bill |
| 20 | Self-checkout | Weighing scale | Weight changed | Checkout software | Verify item weight, or alert attendant |

Systems analysed: **8** (ATM, Microwave, Traffic Light, Video Game, Elevator, Smartphone, Online Shopping, Security Alarm) plus Self-checkout as a 9th.

## Self-Check Questions

**1. What is the difference between an event source and an event listener?**
An event source is the object that *generates* an event (a button, sensor, timer or network socket). An event listener is the object that *waits for* and receives that event so that something can be done in response. The source says "something happened", and the listener is registered to hear it and trigger the handler code.

**2. Can one event source have multiple listeners? Give an example.**
Yes. A single "Add to cart" button on a shopping website can have one listener that updates the cart count, another that shows a "Item added" pop-up, and another that sends analytics data. In Java Swing, you can call `button.addActionListener(...)` several times and every listener is notified when it is clicked.

**3. Can one listener handle events from multiple sources? Give an example.**
Yes. One listener can be registered with several sources. In an elevator, one controller listens to every floor button, the door sensors and the floor sensors. In Swing, one `ActionListener` can be added to many buttons and use `e.getSource()` to tell which one was clicked.
