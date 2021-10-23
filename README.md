# futex_waitv() patches

This repository has a collection of backported patches to add support for the
`futex_waitv()` syscall. It will appear in mainline at Linux 5.16 release.

This syscall is used by [Proton's Wine](https://github.com/ValveSoftware/wine)
to emulate WindowsNT synchronization functions like `WaitForMultipleObjects()`.

To check if something is calling this syscall, you can use
[bpftrace](https://github.com/iovisor/bpftrace). Open a game and then run:

```
bpftrace -e 'tracepoint:syscalls:sys_enter_futex_waitv { printf("%s\n", comm); }'
```

This will print the name of every process that calls `futex_waitv()`.
You need to run a version of Proton that supports this API.

> **Note:** There's not Proton version that supports this yet, but this is
> [work in progress](https://github.com/ValveSoftware/wine/pull/128).

---

All code here is licensed as GPL-2.0.
