This reproduces a bug in the hermetic sandbox where the / directory is writable
by the sandboxed user. (Outside the sandbox, the / directory is owned by root and
not writable by others.)

To repro, install Bazelisk and run `bazelisk test //:test_mkdir`. I did this on
Ubuntu 20.04.

The test will succeed, but it should fail. Run
`bazelisk test --spawn_strategy=local --nocache_test_results //:test_mkdir` to run
it outside the sandbox; it will fail with "mkdir: cannot create directory '/foo': Permission denied".

As another way of looking at it, run `bazelisk test //:test_perms`; you'll see the
difference:

```
==================== Test output for //:test_perms:
1c1
< drwxr-xr-x nobody nogroup
---
> drwxr-xr-x root root
================================================================================
```
