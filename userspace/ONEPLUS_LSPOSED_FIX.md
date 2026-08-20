# OnePlus temporary-root Zygisk lifecycle fix

This fork adds a OnePlus/GhostLock compatibility behavior to the normal non-Magica `ksud late-load` path.

After KernelSU has been late-loaded and the late-load module stages have been prepared, the ReSukiSU Manager app is kept stopped and `ksud soft-reboot` is launched from the root ksud context. The emulated userspace boot then replays the normal post-fs-data/start/service/boot-completed lifecycle so a fresh zygote and system_server can receive Zygisk-based framework injection.

This addresses the observed state where LSPosed/Vector userspace daemons start after GhostLock late-load but cannot establish their system_server bridge until a full ReSukiSU emulated userspace reboot is performed.

The behavior in this fork is intentionally OnePlus/GhostLock-specific; upstream ReSukiSU behavior is not changed here.
