# Event-Driven Programming in Java

My journey learning Event-Driven Programming in Java -



## What this repository covers

Week 1 introduces the fundamentals of event-driven programming (EDP): events, event sources, listeners, handlers, the event queue, the event loop, and the Java Swing Event Dispatch Thread (EDT).

## Repository structure

```
event-driven-programming-java/
├── README.md
├── LICENSE
├── .gitignore
└── Week1_EDP/
    ├── Activity1_Spot_the_Components/
    │   └── EDP_Components.md
    ├── Activity2_Build_the_Event_Loop/
    │   └── EventLoop_Reflection.md
    ├── Activity3_Procedural_vs_EventDriven/
    │   ├── procedural/ProceduralCalculator.java
    │   ├── eventdriven/EventDrivenCalculator.java
    │   └── Comparison_and_Reflection.md
    ├── Activity4_Debug_the_Event_Handler/
    │   ├── Bug1_BlockingEDT.java
    │   ├── Bug2_MissingListener.java
    │   ├── Bug3_WrongThread.java
    │   ├── Bug4_MemoryLeak.java
    │   └── BugFixes.md
    ├── Activity5_Design_Your_Own_System/
    │   ├── SystemDesign.md
    │   └── ParkingGaragePrototype.java
    └── Activity6_Final_Self_Assessment/
        ├── SelfAssessment.md
        └── Summary.md
```

## Activities

| # | Activity | Folder | Outcomes |
|---|----------|--------|----------|
| 1 | Spot the Components | [Activity1_Spot_the_Components](Week1_EDP/Activity1_Spot_the_Components) | #1, #4 |
| 2 | Build the Event Loop | [Activity2_Build_the_Event_Loop](Week1_EDP/Activity2_Build_the_Event_Loop) | #3 |
| 3 | Procedural vs. Event-Driven | [Activity3_Procedural_vs_EventDriven](Week1_EDP/Activity3_Procedural_vs_EventDriven) | #2 |
| 4 | Debug the Event Handler | [Activity4_Debug_the_Event_Handler](Week1_EDP/Activity4_Debug_the_Event_Handler) | #1, #3 |
| 5 | Design Your Own System | [Activity5_Design_Your_Own_System](Week1_EDP/Activity5_Design_Your_Own_System) | #1-#4 |
| 6 | Final Self-Assessment | [Activity6_Final_Self_Assessment](Week1_EDP/Activity6_Final_Self_Assessment) | All |

## Learning outcomes

1. Define the fundamental components of an event-driven system (Event, Source, Listener, Handler)
2. Compare and contrast procedural, functional, and event-driven programming paradigms
3. Explain the role of the event loop and event queue in an event-driven system
4. Identify real-world event-driven systems and their key components

## How to compile and run

Requires a JDK (Java 11 or later). Swing is included with the JDK.

```bash
# Procedural calculator (console)
cd Week1_EDP/Activity3_Procedural_vs_EventDriven/procedural
javac ProceduralCalculator.java
java ProceduralCalculator

# Event-driven calculator (GUI)
cd ../eventdriven
javac EventDrivenCalculator.java
java EventDrivenCalculator

# Bug fix challenge (run any of the four)
cd ../../Activity4_Debug_the_Event_Handler
javac Bug1_BlockingEDT.java
java Bug1_BlockingEDT

# Parking garage prototype
cd ../Activity5_Design_Your_Own_System
javac ParkingGaragePrototype.java
java ParkingGaragePrototype
```

## Key takeaways

1. Never block the Event Dispatch Thread; run long tasks on a background thread.
2. Every interactive component needs a registered listener.
3. Only update Swing components from the EDT (`SwingUtilities.invokeLater`).
4. Remove references to components you no longer need to avoid memory leaks.







