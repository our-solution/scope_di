---
title: Comparison with alternatives
description: Challenges and limitations found in other approaches.
---

Disco was developed to overcome the challenges and limitations of the Flutter ecosystem in the context of dependency injection. Let's understand them together.

### Provider package  

The Provider package, widely used by the Flutter community, injects values into the widget tree based on their type (e.g., `context.get<SomeClass>()`). However, it has notable drawbacks:

- **Shadowing** (i.e., providers with the same type are shadowed by the nearest one)  
  - Solutions like wrapper types or IDs add verbosity or are error-prone (e.g., string-based IDs can cause issues during refactoring).  
- **Lack of compile-time safety**  
  - It's hard to verify if a provider exists for a given type without inspecting the codebase.  
  - Removing a provider doesn't always trigger a static error, risking invalid injections (runtime errors) or, even worse, injections of the wrong provider (of the same type) higher up the tree.  
  - Debugging errors is challenging due to limited information in stack traces.

### Global state management solutions

Due to the limitations mentioned earlier, the Flutter ecosystem saw the emergence of multiple global state management packages. These packages address issues like compile-time safety and shadowing, while also separating business logic from UI. They are usually very advanced (e.g., they can also function as service locators).

However, they introduce new challenges:

- **Unrestricted access**
  - Being able to access everything from everywhere can lead to spaghetti code.
- **Circular dependencies**
- **Local-state-like logic** that doesn't behave exactly like real local state
  - This complicates the logic, especially for beginners.
  - Some solution require objects of special classes to manage the global state.
    - Passing these objects around creates inconsistencies and can feel like working against the framework.
- **Code generation** in some packages  
  - It should not be necessary.
  - Creates a high learning curve for new developers.

## Inspirations and key features

While analyzing the drawbacks of the approaches above, we also drew inspiration from their strengths. Disco combines the best of them, particularly:

- **Scoping from Provider**  
  - It fosters synergy with the widget tree.
  
- **Increased compile-time safety from Riverpod**  
  - Providers are injected via their instance, acting as an identifier, rather than by type.

Disco also emphasizes:

- **Injecting observables/signals directly**  
  - Allows for injecting the observables/signals themselves, enabling loose coupling with third-party state management solutions.
