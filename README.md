# Nexus Protocol Specifications

This repository serves as the **Single Source of Truth (SSoT)** for the data structures, serialization schemas, and Inter-Process Communication (IPC) contracts used across the **Nexus Cybersecurity Suite**. 

By decoupling our schemas from individual applications, we enable seamless polyglot interoperability between ecosystem tools written in **Rust, Go, C#, C++, and Python**.

## Architectural Vision

Instead of utilizing heavy runtime network dependencies or error-prone manual duplicate files, the Nexus Ecosystem uses this centralized repository distributed to other autonomous tools via **Git Submodules**. Code generation happens locally during compile-time for each targeted language.
```bash
              ┌───────────────┐
              │ nexus-protocol│ (Schema Repository)
              └───────┬───────┘
                      │ Distributed via Git Submodules
    ┌─────────────────┼─────────────────┐
    ▼                 ▼                 ▼
    NetSentinel       ShadowDecoy        SleuthHound
(Rust/Iced)     (Python/PySide6)   (C#/.NET/Avalonia)
```

## Core Schema Contract (`nexus_ipc.proto`)

The messaging bus uses **gRPC over Local Sockets** (Unix Domain Sockets on Linux/macOS and Named Pipes on Windows). The current definitions support:
* **Network Discovery Data:** Transmission of audited hosts, open ports, and OS telemetry.
* **Orchestration Triggers:** Cross-tool execution calls (e.g., NetSentinel triggering a local fuzzer).
* **Security & SIEM Alerts:** High-priority internal messaging triggered by deceptive traps or defensive handlers.

## Usage in Autonomous Repositories

To inject this protocol contract into an ecosystem app, add it as a git submodule:

```bash
git submodule add [https://github.com/DanielMR-dev/nexus-protocol](https://github.com/DanielMR-dev/nexus-protocol) proto
```

License
Open Source under the MIT License.
