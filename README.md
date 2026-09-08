# YGOEnv: A Reinforcement Learning Environment for Yu-Gi-Oh!

> **Archived / superseded:** YapCore is no longer an active execution backend. The current project architecture uses [MAPPING](https://github.com/petrademia/mapping) for deck semantics and experiment configuration, [RAPPING](https://github.com/petrademia/rapping) for YGOPro replay ingestion and factual trajectory extraction, and [YAPPING](https://github.com/petrademia/yapping) for legal execution, bounded search, counterfactual analysis, learning, and verification. This repository remains available as historical reference for its vectorized environment and feature representation. It is not maintained and should not be treated as behaviorally equivalent to YAPPING.
>
> No compatibility or conformance with current YAPPING engine pins is guaranteed. Do not treat YapCore and YAPPING transitions or actions as interchangeable. Future high-throughput work should be driven by measured YAPPING bottlenecks rather than automatically reviving this backend.

This repository provides a self-contained Gymnasium-compatible environment for simulating Yu-Gi-Oh! duels using the YGOPro engine.
It was a minimal, maintained fork of the original `ygo-agent` project, stripped down to focus on the environment and engine interface, with some minor differences.

---

## Features

* **Gymnasium-compatible** environment for reinforcement learning research.
* **C++ backend** built via `xmake` for efficient simulation.
* **Supports multiple decks** and locales (English and Chinese).
* **Integrated with official MyCard databases and scripts.**

---

## Requirements

* Linux 
* Python 
* `xmake` 
* System packages: `libsqlite3-dev`, `git`, `build-essential`

---

## Setup Instructions

### 1. Clone the repository

```bash
git clone https://github.com/<your-username>/ygo-env.git
cd ygo-env
```

### 2. Build the environment and fetch card databases and scripts

```bash
xmake f -m release -y
xmake
make
```

This will:
* Download card databases and text files into `assets/locale/en` and `assets/locale/zh`.
* Clone official scripts into `third_party/ygopro-scripts` and link them to `scripts/script`.
NOTE: When you run code that interacts with the environment, for the lua scripts to work a symlink to `third_party/ygopro-scripts` must be in the directory you run the code from. 
### 4. Quick validation

```bash
python - <<'PY'
import ygoenv
print("ygoenv loaded successfully:", ygoenv.__name__)
PY
```

---

## Usage Example

See `example/test_init.py`.

---

## Directory Structure

```
ygo-env/
├── assets/                # Card databases and decks
├── scripts/               # Symlink to ygopro-scripts
├── ygoenv/                # Python package
│   ├── ygoenv/ygopro/     # C++ bindings and wrappers
│   └── python/            # Gymnasium and DM wrappers
├── Makefile               # Build and asset management
├── xmake.lua              # Build rules for xmake
├── setup.py               # Utilized in make script
└── example/               # Example scripts
```

---
## Notes

* The environment is designed for **research use**.
* To add new decks, place `.ydk` files into `assets/deck/`.
* To update scripts or databases, simply re-run `make scripts` or `make assets`.

---

## License

This project inherits the license of the original [ygo-agent](https://github.com/sbl1996/ygo-agent).
Yu-Gi-Oh! and YGOPro are trademarks of their respective owners. This project is for educational and research purposes only.

---
