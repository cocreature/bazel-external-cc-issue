# CC toolchain in external workspace leaks absolute path to execroot

On Windows, rules_haskell uses the msys bundled with GHC as the CC
toolchain. This results in absolute paths to system headers located in
the execroot being included in `.d` files. If these files are cached
and you run the build from different directories (thereby leading to
different execroots), you will get errors as follows:

```
this rule is missing dependency declarations for the following files included by 'main.c':
  'C:/users/admin/_bazel_admin/f7njcwvj/execroot/bazel_dcc_external/external/rules_haskell_ghc_windows_amd64/mingw/x86_64-w64-mingw32/include/stdio.h'
```

I don’t think this issue is limited to Windows but I don’t know an
easy way to setup a CC toolchain in this way on Linux or MacOS.

## Steps to reproduce

1. Clone this repo twice into differently named working directories.
2. Run `bazel build //... --disk_cache C:\Users\yourusername\cache`
   from the first clone.
3. Run `bazel build //... --disk_cache C:\Users\yourusername\cache`
   from the second clone (use the same cache directory).
