I made these `PKGBUILD`s because I found the existing procedures
unsatisfactory. They all fetch directly from GitHub and thus don't
necessarily correspond to any particular release.

- [**`bitcoin-abc`**](./bitcoin-abc) creates (and installs) the `abc-bitcoind`
  daemon for running a [Bitcoin Cash](https://bitcoincash.org) node.
- [**`bitcoin-gold`**](./bitcoin-gold) creates (and installs) the `bgoldd` daemon
  for running a [Bitcoin Gold](https://bitcoingold.org) node. It uses the `0.15`
  branch, so you may change this if necessary.
- [**`litecoin`**](./litecoin) creates (and installs) the `litecoind` daemon
  for running a [Litecoin](https://litecoin.org) node, as well as
  `litecoin-cli`.

To simply install these with the Arch Build System (like on [Arch
Linux](https://archlinux.org), [Manjaro Linux](https://manjaro.org), or
[Parabola GNU/Linux](https://parabola.nu)), use `makepkg`:

```sh
$ cd bitcoin-abc
$ makepkg -sci
```
