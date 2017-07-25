Libre Computer Linux Overlays
=============================

These overlays are designed to work with the 4.12 Linux fork from https://github.com/BayLibre/libretech-linux

Build
=====

You need a "Overlay Enabled" device tree compiler, you can use the following one :

```
$ git clone https://github.com/RobertCNelson/dtc.git dtc --depth 1
$ cd dtc
dtc$ make all
```

Add the `dtc` binary in your PATH then :

```
make
```

Install
=======

Copy the `overlay/*.dtbo` files in the `/lib/firmware` directory of your rootfs.

Copy the `overlay.sh` tool into the `/usr/sbin` directory of your rootfs.

Load
====

```
# mount x /sys/kernel/config -t configfs
```

(if not already mounted)


Then load the overlay (we can only specify part of the filename) :

```
# overlay.sh add libretech-cc-uarta
```
