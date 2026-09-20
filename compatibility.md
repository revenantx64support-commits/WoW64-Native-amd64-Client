# Compatibility

## Overview

WoW64 targets the **World of Warcraft 3.3.5a era** and is being developed as a native AMD64 client.

Compatibility is treated as a collection of independently testable areas rather than as a single binary state.

The project evaluates compatibility progressively as individual client systems become operational and are validated.

---

## Compatibility Targets

The primary target is the client architecture and runtime environment associated with the World of Warcraft 3.3.5a era.

The project focuses on preserving the functional requirements expected by that client environment while replacing the underlying 32-bit execution architecture with a native AMD64 implementation.

```text id="kq4y9s"
World of Warcraft 3.3.5a Era
              │
              ▼
       Compatibility Layer
              │
              ▼
      Native AMD64 Client
```

---

## Compatibility Areas

### Client Runtime

The native client must reproduce the required runtime behavior of the target environment.

Areas include:

- Application initialization
- Runtime lifecycle
- Client state
- Resource management
- Event processing
- System integration

**Current status:** Active development.

---

### Game Data

The client is designed to work directly with packaged game data.

Required resources can be accessed at runtime without first extracting the packaged data into loose files.

```text id="k4xv2s"
Packaged Game Data
        │
        ▼
 Runtime Data Access
        │
        ▼
 Resource Loading
        │
        ▼
 Client Systems
```

**Current status:** Working.

---

### Graphics

Graphics compatibility covers the rendering functionality required by the target client environment.

The architecture separates client systems from the underlying rendering implementation through a graphics abstraction.

The project is designed to provide a path for both legacy rendering compatibility and modern rendering backends.

**Current status:** Active development.

---

### User Interface

UI compatibility includes the client-facing interface and the systems required to initialize and operate it.

The current implementation is capable of reaching the Login Screen.

**Current status:** Login Screen reached; additional UI functionality remains under development.

---

### Networking

Networking compatibility covers communication between the client and compatible server infrastructure.

Relevant areas include:

- Connection handling
- Session state
- Network message processing
- Serialization
- Deserialization
- Client/server state synchronization

**Current status:** Active development.

---

### Authentication

Authentication is part of the compatibility target beyond the current Login Screen milestone.

The current public milestone should not be interpreted as indicating that the complete authentication flow is already implemented.

**Current status:** Next development stage.

---

### Character Systems

Character-related compatibility includes:

- Character selection
- Character creation
- Character data
- Client-side character state

These systems depend on the successful completion of the preceding authentication and session stages.

**Current status:** Future milestone.

---

### World Entry

World-entry compatibility covers the transition from the character/session stages into the game world.

This includes the initialization and synchronization required before normal world interaction can begin.

**Current status:** Future milestone.

---

### Gameplay Runtime

Full gameplay compatibility represents a later stage of development.

It includes the collection of client systems required for normal operation inside the game world.

Potential areas include:

- World state
- Object systems
- Character systems
- Input
- Client-side gameplay logic
- UI interaction
- Rendering
- Networking

**Current status:** Future milestone.

---

## Current Compatibility Matrix

| Area | Current Status |
|---|---|
| Native AMD64 execution | Working |
| Client startup | Working |
| Runtime initialization | Working |
| Packaged game-data access | Working |
| Runtime resource loading | Working |
| Login Screen | Reached |
| Authentication | In development |
| Character selection | Not yet reached |
| Character creation | Not yet reached |
| World entry | Not yet reached |
| Full gameplay runtime | Future milestone |
| Complete client compatibility | Not yet claimed |

The statuses above represent the current development stage and will change as additional systems are implemented and validated.

---

## Compatibility Validation

Compatibility is validated incrementally.

The general process is:

```text id="xqbyf3"
Implementation
     │
     ▼
Build Validation
     │
     ▼
Subsystem Validation
     │
     ▼
Integration Testing
     │
     ▼
Runtime Testing
     │
     ▼
Compatibility Testing
```

A feature is not considered complete solely because the corresponding code builds successfully.

Runtime behavior and interaction with dependent systems are part of the validation process.

---

## Client / Server Compatibility

The project is intended to maintain compatibility with server infrastructure appropriate for the target client environment.

Client/server compatibility is evaluated through actual communication and runtime behavior rather than by assuming that matching protocol definitions alone guarantee compatibility.

The ultimate goal is for the native AMD64 client to operate within an appropriate client/server environment without requiring the original 32-bit client executable.

---

## Data Compatibility

The data layer is designed around runtime access to packaged game data.

This means the client architecture does not require a separate preprocessing stage that extracts all game resources into loose files before execution.

The target model is:

```text id="x0xjbs"
Packaged Files
      │
      ▼
Runtime Access
      │
      ▼
Resource Resolution
      │
      ▼
Decoded / Loaded Resource
      │
      ▼
Client Subsystem
```

The public repository does not contain the proprietary game data required to reproduce this environment.

---

## Native Architecture Compatibility

The central architectural distinction of WoW64 is the execution environment.

The project targets:

```text id="q7s0c2"
Legacy Client Environment
        │
        │  compatibility target
        ▼
Native AMD64 Implementation
```

The objective is not simply to execute the original 32-bit binary through an operating-system compatibility mechanism.

Instead, the project is focused on a native 64-bit client implementation.

---

## What Compatibility Does Not Mean

Compatibility does not imply that the project contains or distributes the original client.

This repository does not provide:

- The original client executable
- Original proprietary game assets
- Extracted game resources
- Proprietary source code
- Reverse-engineering databases
- Raw reverse-engineering datasets

Compatibility refers to the behavior and interfaces being targeted by the independent implementation.

---

## Current Limitations

The current implementation has reached the Login Screen milestone, but substantial client functionality remains to be implemented and validated.

Therefore, the project does not currently claim:

- Complete authentication compatibility
- Complete character-system compatibility
- Complete world-entry compatibility
- Complete gameplay compatibility
- Complete client compatibility

These remain development objectives.

---

## Compatibility Philosophy

The project follows three principles.

### Incremental

Compatibility is developed subsystem by subsystem.

### Observable

Compatibility claims should be supported by observable runtime behavior and testing.

### Explicit

Implemented, partially implemented, planned, and unverified functionality should remain clearly distinguished.

This avoids treating architectural progress as proof of complete client compatibility.

---

## Current Milestone

The current compatibility milestone can be summarized as:

```text id="k6o1v7"
Native AMD64 Client
        │
        ▼
Client Initialization
        │
        ▼
Packaged Data Access
        │
        ▼
Resource Loading
        │
        ▼
Login Screen
        │
        ▼
    NEXT
Authentication
        │
        ▼
Character Systems
        │
        ▼
World Entry
        │
        ▼
Gameplay Runtime
```

Development is currently focused on progressing beyond the Login Screen while maintaining the validated foundations already established.
