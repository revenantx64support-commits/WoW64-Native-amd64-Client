# Current Status

## Overview

**WoW64** is an active research and development project focused on building a native AMD64 client for the World of Warcraft 3.3.5a era.

The project has progressed beyond the initial bootstrap and architectural research stages. The current implementation is capable of starting as a native AMD64 client, accessing packaged game data directly at runtime, loading required resources, and reaching the Login Screen.

---

## Current Milestone

### Login Screen

The current publicly describable milestone is:

```text
Native AMD64 Client
        │
        ▼
Client Startup
        │
        ▼
Runtime Initialization
        │
        ▼
Game Data Access
        │
        ▼
Resource Loading
        │
        ▼
Login Screen
```

The Login Screen represents the current demonstrated endpoint of the client startup sequence.

Further client functionality is under active development.

---

## Current Capabilities

### Native AMD64 Execution

The client is being developed as a native AMD64 application.

The project is not intended to operate by simply running the original 32-bit client through a compatibility layer.

The native architecture is the foundation for the project's long-term development.

### Direct Packaged Data Access

The client can access the game's packaged data files directly during runtime.

Game data does not need to be extracted into loose files before the client can read the required resources.

The general runtime flow is:

```text
Packaged Game Files
        │
        ▼
Data Access Layer
        │
        ▼
Resource Lookup
        │
        ▼
Resource Loading
        │
        ▼
Client Runtime
```

This is an important part of the current implementation because the client is able to work with packaged game data as part of its normal runtime resource-access process.

No game data is included in this public repository.

---

## Current Runtime State

The current implementation has progressed through the early client initialization sequence and can reach the graphical Login Screen.

Current state:

| Area | Status |
|---|---|
| Native AMD64 startup | Active |
| Client initialization | Active |
| Packaged game-data access | Working |
| Runtime resource loading | Working |
| Login Screen | Reached |
| Authentication flow | In development |
| Character selection | Not yet reached |
| Character creation | Not yet reached |
| World entry | Not yet reached |
| Full gameplay runtime | Future milestone |

The table describes the current development state and is expected to change as additional systems become operational.

---

## What Has Been Demonstrated

The current implementation demonstrates several important foundations of the project:

1. The client can execute natively in an AMD64 environment.
2. The client can initialize its runtime.
3. The client can access packaged game data directly.
4. Required resources can be read during runtime without prior extraction.
5. The client can progress far enough to initialize the Login Screen.

These capabilities establish the current foundation for extending the client toward later stages of the original client experience.

---

## Next Development Stages

The next major milestones are expected to extend the client beyond the Login Screen.

### Authentication

The next stage is the integration and validation of the authentication/session flow.

```text
Login Screen
      │
      ▼
Authentication
      │
      ▼
Session Initialization
```

### Character Systems

Following authentication, development will progress toward the character-related client systems.

```text
Authentication
      │
      ▼
Character Selection
      │
      ▼
Character Creation
```

### World Entry

The subsequent milestone is entering the game world and bringing the corresponding client systems online.

```text
Character Selection
      │
      ▼
World Initialization
      │
      ▼
World Entry
```

### Extended Runtime

After world entry, additional systems will be integrated and validated progressively, including world state, objects, gameplay-related client functionality, networking, UI, and other required subsystems.

---

## Validation Approach

The project uses incremental validation rather than treating successful compilation as proof that a subsystem is complete.

The general progression is:

```text
Implementation
     │
     ▼
Build Validation
     │
     ▼
Subsystem Validation
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

A subsystem is considered progressively more mature as it passes increasingly realistic validation stages.

---

## Public Repository Scope

This repository documents the publicly shareable state of the project.

The actual development environment contains material that is intentionally not part of the public repository.

The following are not included:

- Private development source code
- Original proprietary client binaries
- Original proprietary game assets
- Reverse-engineering databases
- Raw reverse-engineering data
- Function addresses and internal offsets
- Binary signatures
- Internal implementation mappings
- Private research reports
- Internal development tools
- Private build artifacts
- Credentials or private server configuration

The public documentation therefore describes the project's architecture, current capabilities, development milestones, and general technical direction without exposing private implementation material.

---

## Current Limitations

The current Login Screen milestone does not represent a complete client.

Important functionality remains to be implemented and validated before the project can progress through the complete client runtime.

In particular, the current public status should not be interpreted as indicating that authentication, character selection, world entry, or full gameplay functionality are already complete.

---

## Status Summary

```text
┌─────────────────────────────────────────┐
│             WoW64 STATUS                │
├─────────────────────────────────────────┤
│                                         │
│ Native AMD64 Client        ✓            │
│ Client Startup             ✓            │
│ Runtime Initialization     ✓            │
│ Packaged Data Access       ✓            │
│ Runtime Resource Loading   ✓            │
│ Login Screen               ✓            │
│                                         │
│ Authentication             → Next       │
│ Character Systems          → Planned    │
│ World Entry                → Planned    │
│ Full Runtime               → Future     │
│                                         │
└─────────────────────────────────────────┘
```

---

## Status Classification

The project is currently classified as:

**Active Research & Development — Login Screen Milestone**

Development continues toward progressively larger portions of the client runtime.

This document should be updated whenever a major publicly demonstrable milestone is reached.
