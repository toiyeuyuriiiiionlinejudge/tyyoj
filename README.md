# Toi Yêu Yuri Online Judge (`tyyoj`)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![GitHub Org](https://img.shields.io/badge/org-toiyeuyuriiiiionlinejudge-purple.svg)](https://github.com/toiyeuyuriiiiionlinejudge)

**Toi Yêu Yuri Online Judge (`tyyoj`)** is a high-security, multi-repository competitive programming online judge platform. It features Administrator-controlled persistent Docker judger worker provisioning, full Markdown + KaTeX math rendering, and multi-mode judging supporting Standard token/diff comparison, Custom Checkers with `testlib.h`, and Interactive tasks with bidirectional POSIX pipes.

---

## Multi-Repository Ecosystem

The `tyyoj` platform is decomposed into modular, public repositories under the [`toiyeuyuriiiiionlinejudge`](https://github.com/toiyeuyuriiiiionlinejudge) organization:

| Repository | Tech Stack | Role & Responsibility |
|---|---|---|
| **[`tyyoj`](https://github.com/toiyeuyuriiiiionlinejudge/tyyoj)** | Docker Compose, Shell | Base orchestrator, local dev infrastructure, unified docs, and deployment manifests. |
| **[`tyyoj-contracts`](https://github.com/toiyeuyuriiiiionlinejudge/tyyoj-contracts)** | Rust 1.99.1, OpenAPI 3.1 | Shared data structures, DTOs, verdict enumerations, and API contracts. |
| **[`tyyoj-backend`](https://github.com/toiyeuyuriiiiionlinejudge/tyyoj-backend)** | Rust (Axum, Tokio, SQLx, Bollard, Lettre) | Core REST API, persistent Docker Judger Engine provisioner, Redis queue dispatcher, and authentication. |
| **[`tyyoj-judger`](https://github.com/toiyeuyuriiiiionlinejudge/tyyoj-judger)** | Rust daemon + C++20 Sandbox | Persistent worker daemon pulling jobs from Redis and executing untrusted submissions inside Linux sandboxes. |
| **[`tyyoj-frontend`](https://github.com/toiyeuyuriiiiionlinejudge/tyyoj-frontend)** | React 19, TypeScript, Vite, TailwindCSS, KaTeX | Web interface for problem viewing with math expressions, code submissions, live verdicts, and Admin Judger fleet control. |

---

## Key Features

1. **Persistent Admin-Controlled Judger Fleet:**
   Judgers do not spawn and terminate ephemerally. Administrators explicitly create, scale, inspect, start, stop, and destroy persistent `tyyoj-judger` container instances via the Admin GUI through the Docker Engine socket API (`bollard`).
2. **Three Supported Contestant Languages:**
   - **C++:** Compiles with `g++ -std=c++20 -O2`.
   - **Pascal:** Compiles with Free Pascal `fpc -O2`.
   - **Python:** Executed with `python3` / `pypy3` inside restricted sandbox.
3. **Three Judging Modes:**
   - **Standard Mode:** Token-by-token whitespace-normalized diff check.
   - **Custom Checker Mode:** Compiles and executes problem-specific testlib checker with `inf`, `ouf`, `ans` streams.
   - **Interactive Mode:** Spawns contestant process and problem interactor simultaneously connected via bidirectional POSIX pipes (`stdin`/`stdout`), enforcing CPU time limits and wall-clock idleness limits (`IDLENESS_LIMIT_EXCEEDED`).
4. **Rich Problem Statements:**
   Problem statements render complete GitHub-flavored Markdown and inline/block KaTeX mathematical formulas (`$...$` and `$$...$$`).
5. **Robust Security & Isolation:**
   Submissions run with `NetworkMode: "none"`, strict cgroups v2 CPU and memory limits, PID bounds, read-only root filesystems, and tmpfs scratch spaces.

---

## Development Setup

See [`docs/dev-setup.md`](docs/dev-setup.md) for complete local setup and Docker Compose instructions.

---

## Authors & License

- **Authors:** toiyeuyuriiiii & nmkdeveloper
- **Copyright:** 2026 Toi Yêu Yuri Online Judge (toiyeuyuriiiii & nmkdeveloper)
- **License:** [MIT](LICENSE)
