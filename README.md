# Go Array Access Bug

## Reproduce the bug

1. Use `nix develop` to get access to the same compiler version as when this bug
   was discovered.
1. Run the program with a debugger: `gdlv debug input`.
1. Watch closely the access to the `rule` variable defined on line 406.
