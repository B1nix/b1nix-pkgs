# b1nix-pkgs

Package repository for [b1nix](https://github.com/B1nix/b1nix), served as static
files over the [jsDelivr](https://www.jsdelivr.com/) CDN — no server to run.

## Layout

```
pkgs/
  index          # text index of available packages (see its header for the format)
  *.tar.gz       # package tarballs, extracted into / on the target
```

## How it's used

On b1nix, `bpkg` reads the index over HTTPS and installs packages:

```sh
bpkg update            # fetch pkgs/index
bpkg install <name>    # download + sha256-verify + extract the tarball
bpkg list / remove / search
```

Default index URL (jsDelivr over this repo's `main`):

```
https://cdn.jsdelivr.net/gh/B1nix/b1nix-pkgs@main/pkgs/index
```

## Publishing

Packages are built with the b1nix cross-toolchain and published from the main
b1nix repo via `tools/bpkg-publish.sh`, which appends to `pkgs/index` and drops
the tarball here. Commit + push, then jsDelivr serves it (note: `@main` is CDN-
cached ~12h; for instant updates pin a tag like `@v1` or purge the URL).
