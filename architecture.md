# WoW64 Architecture

## Overview

WoW64 is designed as a native AMD64 client architecture targeting the World of Warcraft 3.3.5a era.

The project separates platform-specific functionality, runtime systems, data access, graphics, user interface, networking, and higher-level client systems into distinct architectural layers.

The primary objective is to provide a native 64-bit foundation while preserving the functional and behavioral requirements of the target client environment.

---

## High-Level Architecture

```text
┌─────────────────────────────────────────────────────────────┐
│                    Native AMD64 Client                      │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                     Client Systems                          │
│                                                             │
│   Gameplay │ World │ Objects │ Characters │ Input │ UI     │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                  Client Runtime Layer                       │
│                                                             │
│      Events │ Scheduling │ State │ Services │ Messaging     │
│                                                             │
├───────────────────────┬─────────────────────────────────────┤
│                       │                                     │
│      Data Layer       │            Graphics Layer            │
│                       │                                     │
│  Archives / Resources │       Rendering Abstraction         │
│  Data Formats         │                                     │
│  Resource Management  │        ┌────────┬────────┐          │
│                       │        │ D3D9   │ D3D12  │          │
├───────────────────────┴────────┴────────┴───────────────────┤
│                                                             │
│                    Platform Layer                           │
│                                                             │
│       Memory │ Threads │ Filesystem │ Timing │ OS APIs      │
│                                                             │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│                    Native AMD64                             │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

---

## Architectural Principles

### Native 64-bit Execution

The client is designed as a native AMD64 application rather than relying on a 32-bit compatibility environment.

This allows the architecture to use the native 64-bit execution environment and modern operating-system facilities directly.

### Layered Design

Subsystems are separated into logical layers with defined responsibilities.

This reduces coupling between platform-specific functionality and higher-level client systems and allows individual components to be developed and validated independently.

### Runtime Resource Access

Game resources are accessed through a dedicated data layer.

The architecture supports reading packaged game data directly at runtime rather than requiring the data to be extracted into loose files beforehand.

```text
Packaged Game Data
        │
        ▼
 Archive / Data Access
        │
        ▼
 Resource Management
        │
        ▼
 Client Systems
```

The repository does not contain proprietary game data.

### Rendering Abstraction

Graphics functionality is separated from higher-level client systems through a rendering abstraction layer.

This allows the client architecture to maintain compatibility with legacy rendering requirements while providing a path toward modern graphics APIs.

Conceptually:

```text
                 Client Graphics
                       │
                       ▼
                Rendering API
                  Abstraction
                       │
             ┌─────────┴─────────┐
             ▼                   ▼
           D3D9                D3D12
```

The abstraction is intended to prevent higher-level client systems from depending directly on a single graphics backend.

---

## Core Layers

### 1. Native AMD64 Bootstrap

The bootstrap layer is responsible for establishing the native application environment and initializing the client runtime.

Responsibilities include:

- Process initialization
- Runtime initialization
- Platform initialization
- Initial configuration
- Startup sequencing
- Initialization of core services

---

### 2. Platform Layer

The platform layer provides operating-system and hardware-facing functionality required by the client.

Typical responsibilities include:

- Memory management
- Threading
- Synchronization
- Timing
- Filesystem access
- Window management
- Input interfaces
- Operating-system integration

Higher-level systems should interact with these facilities through defined interfaces rather than depending directly on platform-specific implementations.

---

### 3. Runtime Layer

The runtime layer coordinates the execution of the client.

Its responsibilities include:

- Service initialization
- Event processing
- Scheduling
- State management
- Inter-system communication
- Runtime lifecycle
- Error handling

The runtime provides the foundation on which higher-level client systems operate.

---

### 4. Data Layer

The data layer provides access to packaged game resources.

Its responsibilities include:

- Archive access
- File lookup
- Resource loading
- Resource lifetime management
- Data format handling
- Caching where appropriate

The target design allows resources to remain inside their packaged data containers while being accessed by the running client.

---

### 5. Graphics Layer

The graphics layer provides rendering services to the client.

Its responsibilities include:

- Device initialization
- Rendering resources
- Texture management
- Buffer management
- Render-state management
- Presentation
- Graphics synchronization

A rendering abstraction separates these responsibilities from higher-level client logic.

---

### 6. User Interface Layer

The UI layer provides the graphical interface required by the client.

It is responsible for systems such as:

- Interface initialization
- UI resources
- Input interaction
- UI state
- Layout
- Client-facing screens

The current development milestone demonstrates the ability to reach the Login Screen.

---

### 7. Networking Layer

The networking layer provides communication between the client and compatible server infrastructure.

Responsibilities include:

- Connection management
- Packet processing
- Serialization
- Deserialization
- Session state
- Network event handling

Networking functionality is developed independently from the rendering and presentation systems.

---

### 8. Client Systems

The upper layer contains the systems that implement client-side game functionality.

Depending on the development stage, these systems include:

- World management
- Object management
- Character systems
- Input handling
- Gameplay-related client logic
- UI interaction
- Client state

These systems consume services provided by the lower architectural layers.

---

## Startup Flow

The current startup architecture can be represented as:

```text
Application Start
       │
       ▼
AMD64 Bootstrap
       │
       ▼
Platform Initialization
       │
       ▼
Runtime Initialization
       │
       ▼
Data System Initialization
       │
       ▼
Graphics Initialization
       │
       ▼
Client UI Initialization
       │
       ▼
Login Screen
```

This represents the currently demonstrated stage of development.

Further stages will extend the runtime beyond the Login Screen toward authentication, character selection, character creation, and world entry.

---

## Resource Flow

Resources are intended to remain in their packaged form during normal client operation.

```text
              Packaged Data
                    │
                    ▼
             Data File Access
                    │
                    ▼
              File Lookup
                    │
                    ▼
            Resource Loading
                    │
                    ▼
             Resource Cache
                    │
                    ▼
             Client Subsystem
```

The exact internal implementation of the data system is intentionally not documented in this public repository.

---

## Graphics Flow

The graphics architecture follows a layered model:

```text
Client Systems
      │
      ▼
Graphics Services
      │
      ▼
Rendering Abstraction
      │
 ┌────┴────┐
 ▼         ▼
D3D9      D3D12
```

This design allows graphics implementation details to remain isolated from the rest of the client.

---

## Runtime Validation

Each major architectural layer is intended to be validated independently before being relied upon by higher-level systems.

The general validation model is:

```text
Component
    │
    ▼
Unit / Subsystem Validation
    │
    ▼
Integration Validation
    │
    ▼
Runtime Validation
    │
    ▼
Compatibility Validation
```

Successful compilation alone is not considered sufficient validation.

---

## Current Architectural Milestone

The current implementation has reached the following stage:

```text
Native AMD64 Startup             [Active]
        │
        ▼
Platform Initialization          [Active]
        │
        ▼
Runtime Initialization           [Active]
        │
        ▼
Packaged Data Access              [Active]
        │
        ▼
Resource Loading                  [Active]
        │
        ▼
Graphics / UI Initialization      [Active]
        │
        ▼
Login Screen                      [Reached]
        │
        ▼
Authentication                    [Next]
        │
        ▼
Character Systems                 [Planned]
        │
        ▼
World Entry                       [Planned]
```

The status of individual components may change as development progresses.

---

## Public Repository Scope

This document describes the public architectural model of the project.

It intentionally does not expose:

- Reverse-engineering databases
- Raw reverse-engineering results
- Function addresses
- Memory offsets
- Binary signatures
- Internal implementation mappings
- Private source code
- Proprietary game data
- Internal development tooling

The public architecture describes **what the system does and how its major components relate to one another**, rather than exposing private implementation details.

---

## Future Architecture

The architecture is designed to remain extensible beyond the initial compatibility target.

Potential future areas include:

- Additional rendering backends
- Modern graphics capabilities
- Expanded hardware support
- Improved resource management
- Performance-oriented subsystems
- Additional development tooling
- Extended client functionality

The architecture may evolve as research and implementation progress.

---

## Summary

WoW64 is structured as a native AMD64 client architecture with clearly separated platform, runtime, data, graphics, UI, networking, and client-system layers.

The current implementation has progressed to a functional Login Screen milestone and is capable of accessing packaged game data directly at runtime without requiring prior extraction.

The public repository documents this architecture and its development progress while keeping private implementation details and reverse-engineering materials outside the public project.
