# asuka-git

AUR sources for [unmellow/asuka](https://github.com/unmellow/asuka), a
fork of [~julienxx/asuka](https://git.sr.ht/~julienxx/asuka) that uses
Cursive 0.21 with the **crossterm** backend. It does **not** depend on
ncurses.

The release tarball [AUR/asuka](https://aur.archlinux.org/packages/asuka)
(vladimyr) is still upstream 0.8.5 + ncurses. Both may coexist as
`asuka` vs `asuka-git`; they `conflicts` with each other.

Packaging follows:

- [AUR submission guidelines](https://wiki.archlinux.org/title/AUR_submission_guidelines)
- [Rust package guidelines](https://wiki.archlinux.org/title/Rust_package_guidelines)
- [VCS package guidelines](https://wiki.archlinux.org/title/VCS_package_guidelines)

Package sources (`PKGBUILD` and helpers) are licensed 0BSD (`LICENSE`, `REUSE.toml`).
Upstream asuka remains MIT.

## Build

```bash
sudo pacman -S --needed base-devel git cargo openssl
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
git commit -m "asuka-git: Cursive 0.21 / crossterm; drop ncurses"
git push
```
