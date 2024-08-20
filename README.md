# aarch64-alire-index
> Alire port to aarch64 (Linux)

This repository is a draft port of [Alire](https://alire.ada.dev/) to `aarch64` Linux platform.
This works in particular on Ubuntu 22.04 and [Raspberry Pi 64-bits](https://ubuntu.com/download/raspberry-pi).

## Install

1. Download `alr` and add it to the `PATH` environment variable:

```
wget https://github.com/reznikmm/aarch64-alire-index/releases/download/v2.0.1/alr-2.0.1-bin-aarch64-linux.zip
unzip alr-2.0.1-bin-aarch64-linux.zip
export PATH=$PWD/bin:$PATH
```

2. Clone and setup `aarch64-alire-index`:

```
alr index --reset-community
alr index --add git+https://github.com/reznikmm/aarch64-alire-index.git \
  --name aarch64 --before community
```

3. Install Aarch64 GNAT and `gprbuild`:

```
alr toolchain --select gnat_native=14.2.1 gprbuild=22.0.1
```

4. Done! Use `alr` as usual:
```
alr get --build hello
```

## Use in continue integration (CI)

The [Circle CI](https://circleci.com/docs/2.0/arm-resources/) has an ARM
machine executor in a free plan.
To use it add a `.circleci/config.yml` YAML configuration, like this:

```yaml
version: 2.1

jobs:
  say-hello:
    resource_class: arm.medium
    machine:
      image: cimg/base:current-22.04
    steps:
      - checkout
      - run:
          name: "Build with alr"
          command: |
             curl -O -L https://github.com/reznikmm/aarch64-alire-index/releases/download/v2.0.1/alr-2.0.1-bin-aarch64-linux.zip
             unzip alr-2.0.1-bin-aarch64-linux.zip
             export PATH=$PWD/bin:$PATH
             alr index --reset-community
             alr index --add https://github.com/reznikmm/aarch64-alire-index.git --name aarch64 --before community
             alr toolchain --select gnat_native=14.2.1 gprbuild=22.0.1
             alr build
workflows:
  say-hello-workflow:
    jobs:
      - say-hello
```

## Maintainer

[Max Reznik](https://github.com/reznikmm).

## Contribute

Feel free to dive in! Visit the [chat](https://gitter.im/ada-lang/Alire).
[Open an issue](https://github.com/reznikmm/aarch64-alire-index/issues/new)
or submit PRs.

## License

[GPL-3](LICENSE) © Max Reznik
