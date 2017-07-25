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

UART A
------

TX will be on 7J1 Header Pin 8
RX will be on 7J1 Header Pin 10
CTS will be on 7J1 Header Pin 16
RTS will be on 7J1 Header Pin 18

```
# overlay.sh add libretech-cc-uarta
```

To enable a serial console on it :
```
# systemctl enable serial-getty@ttyAML1.service
# systemctl start serial-getty@ttyAML1.service
```

I2C AO
------

SDA will be on 7J1 Header Pin 3
SCL will be on 7J1 Header Pin 5

```
# overlay.sh add libretech-cc-i2c-ao
```

To scan available I2C devices :
```
# i2cdetect -y 1
```

To add a simple device, here a DS3231 RTC module :

```
# echo "ds3231 0x68" > /sys/class/i2c-adapter/i2c-1/new_device
```

I2C B
-----

SDA will be on 7J1 Header Pin 27
SCL will be on 7J1 Header Pin 28

```
# overlay.sh add libretech-cc-i2c-b
```

To scan available I2C devices :
```
# i2cdetect -y 2
```

To add a simple device, here a DS3231 RTC module :

```
# echo "ds3231 0x68" > /sys/class/i2c-adapter/i2c-2/new_device
```

SPICC
-----

MOSI will be on 7J1 Header Pin 19
MISO will be on 7J1 Header Pin 21
CLK will be on 7J1 Header Pin 23
CS0 will be on 7J1 Header Pin 24

```
# overlay.sh add libretech-cc-spicc
```
