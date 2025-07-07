# macOS Rootkit Scaffold

⚠️ **WARNING: For educational use only. Do not deploy on unauthorized systems.**

Implements:
- DKOM for process hiding
- Launchd job unlinking
- Privilege escalation via task patching
- Kernel memory access
- Unsigned KEXT loading (pre-10.10)

# macOS Rootkit Scaffold

⚠️ **WARNING: For educational and research use only. Do not deploy on unauthorized systems. Misuse may violate laws and result in criminal charges.**

## 🧬 Overview

This project provides a modular scaffold for building and testing macOS rootkit components. Inspired by Team T5's "You Can't See Me" paper, it demonstrates stealth techniques on legacy macOS systems.

> Target: macOS 10.6–10.14 (pre-SIP)

---

## 🛠️ Features

- 🔍 **DKOM (Direct Kernel Object Manipulation)** — Unlinks process structures (`p_list`, `p_hash`) to hide from standard enumeration
- 🧼 **Launchd Job Unlinking** — Edits `launchd` memory to remove visibility of daemon jobs
- 🧬 **Host Privilege Escalation** — Modifies `itk_host` to escalate task privileges
- 🧠 **Kernel Memory Access** — Reads/writes remote kernel task memory
- 🧱 **Unsigned KEXT Loader** — Loads unverified kernel extensions from disk or memory (macOS ≤ 10.9)
- 🧩 **Remote dylib Injection** — Injects dynamic libraries into arbitrary PIDs
- 👣 **Log Cleaner** — Erases user/system logs, audit trails, and crash reports
- 🔒 **Filesystem Stealth** — Hooks `readdir()` to hide files by pattern

---

## 📁 Project Structure

```
macos_rootkit/
├── dkom/                 # Process hiding via DKOM
├── launchd/              # launchd memory unlinks
├── privilege/            # Host privilege escalation
├── kernel_access/        # Kernel memory R/W
├── loader/               # KEXT loader + syscall stub
├── root_escalation/      # SMJobBless root access attempt
├── stealth/              # Log cleaner & FS hook
├── utils/                # dylib injector, symbol resolver
├── docs/                 # Architecture and reference
├── build/                # Compiled outputs
```

---

## ✅ Requirements

- macOS (10.6–10.14)
- Xcode CLI tools (`xcode-select --install`)
- SIP and AMFI disabled (or bypassed)
- Root or `task_for_pid` entitlement

---

## 🔧 Usage Examples

### Hide a Process via DKOM
```bash
sudo ./build/hide_proc 1337
```

### Load an Unsigned KEXT
```bash
sudo ./loader/mykextload /path/to/rootkit.kext
```

### Inject a Dylib into Process
```bash
sudo ./utils/inject_dylib 1234 /tmp/inject.dylib
```

---

## ⚠️ Legal Notice

This software is intended solely for lawful research and educational purposes. Use only on systems you own or are authorized to test. The author assumes no liability for misuse.

---

## 📬 Contact

Team T5 (originating concept): [tt@teamt5.org](mailto:tt@teamt5.org)

Current scaffold by: [@phntmzn](https://github.com/phntmzn)
