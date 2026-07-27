# Aqua

**Status: early architecture stage — not yet usable.**

Aqua is a metaprogramming-focused systems language built around one core idea: giving the compiler pipeline itself (tokens, AST nodes, and codegen) the ability to execute code at compile time, so the language, its syntax, and its output targets can be redefined from within the language.

The main scenario Aqua is designed for is bringing multi-language projects into a single shared codebase. Because code generation targets are themselves defined and extendable inside Aqua, the same source can emit C, GLSL, Rust, or other targets depending on which codegen a given AST node resolves to — and users can build their own DSLs on top of the same mechanism.

This repository currently exists as a placeholder for two things:

- `VersionInfo.json` — the versioning/compatibility contract between the compiler and the Language Core (see below)
- `Core/` — where the Language Core (rule definitions, token/AST/semantic specifications) will live once designed

No compiler code lives in this repo yet. This is intentionally an empty shell to lock in the versioning standard early, before the real implementation is pushed.

## Architecture, briefly

Aqua's compiler pipeline is split into independent modules (Lexer, Parser, Source Analyzer, Semantic Analyzer, Generator, Builder, Box/Aqua.py orchestrator) with no hardcoded language rules — every rule, token definition, and semantic behavior is supplied by the **Language Core**. This is what makes the compiler itself language-agnostic: distributing a new "language" is just distributing a new Core.

A full architecture write-up will be added to `docs/` once the Language Core design is finalized.

## Versioning

`VersionInfo.json` exists to let the compiler verify, at boot, that:
- the Language Core it's about to load is compatible with the current compiler version
- the required Core files are actually present
- the Core's own version is being tracked independently of the compiler's version

See the file itself for the current schema.

## License

GPLv3. See `LICENSE`.

> Note: since Aqua is a compiler, GPLv3 governs the compiler's own source code. It does not automatically extend to code *generated* by Aqua unless compiled output embeds Aqua-licensed runtime code — a distinction GCC handles via its own runtime exception. This repo doesn't yet ship a runtime, so it isn't a concern today, but it's worth revisiting once one exists. This isn't legal advice — worth a real look before the first public release.

## Status

Single-developer, early design phase. Architecture and prior language work (Nebula) are being used as design references but not carried over as code. Not accepting contributions yet — this will change once the core pipeline is functional.
