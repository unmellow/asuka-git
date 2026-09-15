# asuka-git

AUR sources for [asuka](https://git.sr.ht/~julienxx/asuka), a Gemini client.
This is the `-git` variant; the release tarball is
[AUR/asuka](https://aur.archlinux.org/packages/asuka) (vladimyr). Both may
coexist.

Packaging follows:

- [AUR submission guidelines](https://wiki.archlinux.org/title/AUR_submission_guidelines)
- [Rust package guidelines](https://wiki.archlinux.org/title/Rust_package_guidelines)
- [VCS package guidelines](https://wiki.archlinux.org/title/VCS_package_guidelines)

Package sources (`PKGBUILD` and helpers) are licensed 0BSD (`LICENSE`, `REUSE.toml`).
Upstream asuka remains MIT.

`RUSTUP_TOOLCHAIN=stable` is set so a rustup install without a default
toolchain no longer fails the build. `gcc` / `pkgconf` come from `base-devel`.

## Build

```bash
sudo pacman -S --needed base-devel git cargo ncurses openssl
makepkg -Csi
```

## Publish to aur.archlinux.org

You already maintain [asuka-git](https://aur.archlinux.org/packages/asuka-git).
AUR only accepts the `master` branch. Do not commit mere `pkgver` bumps.

```bash
git -c init.defaultBranch=master clone ssh://aur@aur.archlinux.org/asuka-git.git
cp PKGBUILD .SRCINFO LICENSE REUSE.toml README.md asuka-git/
mkdir -p asuka-git/LICENSES
cp LICENSES/0BSD.txt asuka-git/LICENSES/
cd asuka-git
makepkg --printsrcinfo > .SRCINFO
git add PKGBUILD .SRCINFO LICENSE REUSE.toml LICENSES README.md
git commit -m "asuka-git: follow AUR, VCS, and Rust package guidelines"
git push
```
