# Gotchas

Sharp edges in the lab environment. Read before building.

## Never bridge the target VM

Metasploitable 2 is a deliberately vulnerable machine with default credentials and
remotely exploitable services on nearly every open port. Bridged networking places it
directly on the home LAN, reachable by every device on it — and reachable *from* it.
This is a real risk, not a theoretical one.

- **Target VM:** host-only adapter, one adapter, no NAT, no bridge. It never needs
  internet access.
- **Kali VM:** host-only adapter on the same isolated network, *plus* a second NAT
  adapter for updates and package installs.
- Snapshot both VMs clean immediately after install, before the first exercise.

## Hyper-V is on, and it changes how VMs run

`HypervisorPresent` is `True` because WSL2 (Ubuntu) and Docker Desktop are installed
and in use. Hyper-V therefore owns the bare-metal virtualisation layer, and VMware
Workstation runs on top of it through the Windows Hypervisor Platform rather than
against the CPU directly.

- Expect a performance penalty on every VM. On a Ryzen 5 5600X with 32 GB it should be
  tolerable; if it is not, see the fallback in
  [ADR 0001](adr/0001-vmware-workstation-lab.md).
- **Do not disable Hyper-V to reclaim the performance.** It breaks WSL2 and Docker
  Desktop, both in active use by other projects.
- Symptoms of the coexistence path going wrong are usually VM start failures or severe
  slowness, not subtle misbehaviour — so it fails loudly, which is good.

## Storage

VMs go on `E:` (223 GB free). Keeps multi-gigabyte disk images and snapshot trees off
the system drive, where `C:` has 250 GB free but is shared with everything else.

## Lab sheets will say VirtualBox

Course material almost always assumes VirtualBox. VMware takes the same `.ova` and
`.vmdk` inputs, so imports work, but menu paths, network-mode names and adapter
settings will not match the instructions verbatim. The mapping to know:

| VirtualBox | VMware Workstation |
|---|---|
| Host-only Adapter | Custom (VMnet1), host-only |
| NAT | NAT (VMnet8) |
| Bridged Adapter | Bridged — **do not use for the target** |
