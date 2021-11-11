# aarch64-alire-index
> Alire port to aarch64

This repository is a draft port of [Alire](https://alire.ada.dev/) to `aarch64` platform.
This works in particular on [Raspberry Pi 64-bits](https://ubuntu.com/download/raspberry-pi).

## Install

1. Download `alr` and add it to the `PATH` environment variable:

```
wget https://github.com/reznikmm/aarch64-alire-index/releases/download/v1.1.1/alr-1.1.1-bin-aarch64-linux.zip
unzip alr-1.1.1-bin-aarch64-linux.zip
export PATH=$PWD/bin:$PATH
```

2. Clone and setup `aarch64-alire-index`:

```
git clone https://github.com/reznikmm/aarch64-alire-index.git
alr index --reset-community
alr index --add file://$PWD/aarch64-alire-index --name aarch64 --before community
```

3. Install Aarch64 GNAT and `gprbuild`:

```
alr toolchain --select gnat_native=11.2.2 gprbuild=21.0.2
```

4. Done! Use `alr` as usual:
```
alr get --build hello
```

## Maintainer

[Max Reznik](https://github.com/reznikmm).

## Contribute

Feel free to dive in! Visit the [chat](https://gitter.im/ada-lang/Alire).
[Open an issue](https://github.com/reznikmm/aarch64-alire-index/issues/new)
or submit PRs.

## License

[GPL-3](LICENSE) © Max Reznik
