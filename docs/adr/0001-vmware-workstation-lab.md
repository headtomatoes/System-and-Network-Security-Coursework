# The lab runs on VMware Workstation Pro, with Hyper-V left enabled

## Context

The prep plan allocates ~4 of ~17 available hours to standing up a Lab that must
survive the whole module. Host is a Ryzen 5 5600X, 32 GB RAM, 250 GB free on `C:`
and 223 GB free on `E:` — hardware is not a constraint here; **hypervisor
coexistence is**.

`HypervisorPresent` is `True` because WSL2 (Ubuntu) and Docker Desktop are both
installed and in use. Hyper-V therefore owns the bare-metal virtualisation layer,
and any type-2 hypervisor has to run on top of it via the Windows Hypervisor
Platform (WHP) rather than against the CPU directly. Disabling Hyper-V would
reclaim that performance but break WSL2 and Docker Desktop, which are in active
use for other projects — so it is not on the table.

Candidates considered: VMware Workstation Pro, VirtualBox, native Hyper-V, and a
Docker-only lab.

## Why

- **Interoperability beats raw speed.** University lab material is distributed as
  `.ova`/`.vmdk` almost universally. Native Hyper-V is the fastest option here (it
  already owns the metal) but every course-issued image would need conversion, its
  virtual-switch model is clunkier for ARP-spoofing/MITM work, promiscuous capture
  is awkward, and essentially no community walkthrough targets it. That is a whole
  term spent off the beaten path to save time we are not short of.
- **VMware over VirtualBox.** Both take the same `.ova` input and both must run
  under WHP. VMware Workstation 17.6 handles WHP coexistence noticeably better than
  VirtualBox 7.x, which is measurably slower and historically flakier in that mode.
  Broadcom made Workstation Pro free for personal use in late 2024, so VirtualBox's
  cost advantage no longer exists. The residual cost is one extra install and being
  one step off what a lab sheet literally says.
- **Docker rejected as the primary lab.** Containers are fast, disposable and cheap
  on disk, and per-container network namespaces do make ARP spoofing and inter-container
  capture genuinely work. But the shared host kernel rules out kernel-level,
  netfilter/iptables, driver and boot-level exercises, and there is no realistic
  whole-machine target. Docker stays available as a fast way to spin up individual
  vulnerable services; it is not the lab.

## Consequences

- Lab VMs live on `E:` (223 GB free, and keeps them off the system drive).
- Accept a WHP performance penalty on every VM. On this CPU/RAM it is expected to be
  tolerable; if it is not, the fallback is native Hyper-V, which would mean converting
  images and abandoning `.ova` interop — i.e. this ADR would be superseded, not
  quietly worked around.
- **Contingent on the syllabus, which has not been read yet.** If the module mandates
  a specific hypervisor or ships pre-built images for one, follow the module and
  supersede this ADR. Interop with course material was the deciding argument, so
  losing that argument reverses the decision.
