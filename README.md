<img width="1254" height="1254" alt="LOGO" src="https://github.com/user-attachments/assets/fd45ad4b-cd2d-43e0-a284-7b826beb83ac" />
<img width="1268" height="716" alt="Screenshot_000003" src="https://github.com/user-attachments/assets/a688eb2e-355a-4a15-928e-018d8958b810" />


## Project Status

**Status: Active Research & Development**

The project has progressed beyond the initial architectural stage and is currently capable of reaching the **Login Screen** in a native AMD64 environment.

Current demonstrated capabilities include:

- Native AMD64 client startup
- Client initialization
- Direct access to game data files
- Runtime reading of game resources without extracting them beforehand
- Login Screen initialization
- Integration of the core systems required to reach the graphical client interface

The implementation is being developed incrementally, with additional client systems being brought online and validated progressively.

## Asset & Data Access

The client is designed to work directly with the game's packaged data files.

Game data does **not** need to be manually extracted into loose files before being accessed by the client.

At a high level, the data flow is:

```text
Game Data Files
       │
       ▼
   Data Reader
       │
       ▼
 Resource Access
       │
       ▼
 Client Subsystems
```

This approach follows the general runtime model expected from the original client architecture, where packaged game data can be accessed directly during execution.

No proprietary game data is included in this repository.

## Current Demonstration

The current implementation can progress through the client startup process and reach the Login Screen.

Conceptually:

```text
Native AMD64 Bootstrap
          │
          ▼
   Platform / Runtime
          │
          ▼
   Client Initialization
          │
          ▼
   Data File Access
          │
          ▼
   Resource Loading
          │
          ▼
      Login Screen
```

This represents the current public development milestone.

## Development Roadmap

### Current Milestone

- [x] Native AMD64 bootstrap
- [x] Core client initialization
- [x] Direct packaged-data access
- [x] Runtime resource loading
- [x] Login Screen
- [ ] Login/authentication flow
- [ ] Character selection
- [ ] Character creation
- [ ] World entry

### Client Systems

- [x] Initial asset/data pipeline
- [ ] Extended data systems
- [ ] Complete graphics pipeline
- [ ] UI systems
- [ ] Scripting integration
- [ ] Networking systems
- [ ] World-state processing

### Compatibility

- [x] Client startup
- [x] Login Screen initialization
- [ ] Authentication
- [ ] Character systems
- [ ] World entry
- [ ] World-state processing
- [ ] Gameplay systems
- [ ] Extended compatibility validation

### Future Development

- [ ] Modern rendering backend
- [ ] Expanded hardware support
- [ ] Performance improvements
- [ ] Extended tooling
- [ ] Advanced client capabilities
