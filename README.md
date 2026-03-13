# PureBSD

> A pure, reproducible, and isolated microkernel-based FreeBSD distribution.

## Philosophy

PureBSD is built on three core principles:

- **Purity** — Every component is immutable. Nothing is modified in place; changes produce new versions. Inspired by the functional programming philosophy of Haskell and Idris2.
- **Reproducibility** — The same configuration always produces the same result, on any machine, at any time. No hidden state, no surprises.
- **Isolation** — Every program runs inside its own microkernel. Each microkernel is the sole gateway between the program and the system. Nothing leaks.

## Architecture

PureBSD is built around a **kernel tree**:

```
Mother Kernel (root)
├── Heavy Microkernel       — manages drivers, multiple programs, shared resources
└── Light Microkernel       — bound to a single program, exists only for that program
    ├── Program A ←→ its own Light Microkernel
    ├── Program B ←→ its own Light Microkernel
    └── Program C ←→ its own Light Microkernel
```

The **Mother Kernel** is the single source of truth. It manages:
- **Public layer** — non-sensitive information, transparent to all child microkernels
- **Private layer** — sensitive system data, accessible only with proper permissions

Child microkernels never talk to each other directly. All communication flows through the Mother Kernel via a structured IPC system.

## Goals

- Modify the FreeBSD kernel to support this microkernel tree architecture
- Build a declarative, reproducible package manager in **Idris2** — fixing the known pain points of NixOS (poor error messages, hidden state, impure builds)
- Support Linux application compatibility inside isolated microkernels, without modifying the applications themselves
- Adaptive runtime: lightweight monolithic mode on constrained hardware, full microkernel mode on capable hardware

## The Lego Philosophy

PureBSD is not here to kill the joy of tinkering.

The goal is the opposite — by giving you a clean, pure, and well-structured base, PureBSD lets you build your system exactly the way you want it, like Lego blocks. Snap what you need, remove what you don't, reshape it however you like.

Purity is not a cage. It is the foundation that makes real freedom possible. You know exactly what every piece does, nothing is hidden, and nothing breaks unexpectedly when you change something.

This is a system for people who actually enjoy building things their own way.

## Why FreeBSD?

FreeBSD provides a clean, well-documented, and unified base (kernel + userland) that is ideal for this kind of low-level experimentation. PureBSD starts from this solid foundation and builds upward.

## Why Idris2?

The package manager and all new components written for PureBSD use **Idris2** — a language with dependent types and no garbage collector. This allows us to:
- Formally verify that configurations are correct before applying them
- Guarantee resource safety without a GC
- Produce something genuinely new, not just a reimplementation of existing tools

## Status

🔴 Early design phase — reading, learning, and planning.

Current focus: *Operating Systems: Three Easy Pieces* → FreeBSD Architecture Handbook → first kernel modifications.

## License

BSD 2-Clause License. See [LICENSE](LICENSE).

## Contributing

PureBSD is open source and welcomes contributions. All ideas, feedback, and pull requests are appreciated.
