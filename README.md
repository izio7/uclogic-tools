Huion-tools
===========

Huion-tools is a collection of programs for collecting and analyzing
diagnostic information from Huion graphics tablets.

Installation
------------

Requirements:

* libusb >= 1.0

Libusb development packages are usually named `libusb-1.0-0-dev` or
`libusbx-devel`.

To build from a distribution tarball the usual `./configure && make`
is sufficient.

To build from the Git tree autotools are required and `./bootstrap &&
./configure && make` is sufficient.

To install huion-tools, use `make install`.

Usage
-----

Huion-tools contains two utilities: huion-probe and huion-decode.

Huion-probe dumps diagnostics information from Huion graphics tablets and, as
a side effect, enables their proprietary mode.

Huion-decode attempts to extract tablet parameters from the information dumped
by huion-probe.

Huion-probe accepts two arguments: bus number and device address. You can find
them in `lsusb` output by looking for a device with vendor ID 256c and product
ID 006e.

For example, in this `lsusb` output:

    Bus 001 Device 003: ID 256c:006e  
    Bus 001 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
    Bus 002 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
    Bus 003 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
    Bus 004 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
    Bus 005 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
    Bus 006 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub

The first line corresponds to a Huion tablet, and so its bus number is 1,
device address is 3 and you probe it like this:

    huion-probe 1 3

The output will be something like this:

    S 64  00 7D 20 4E 03 00 FF 07 A0 0F 08 00 00 00 00 00
    S 65  20 A0
    S 6E  00 30
    S 79  4D 00 35 00 30 00 38 00
    S 7A  01 00 00 00 00 00

Huion-decode simply expects huion-probe output on its input. For the
diagnostics dump above it will produce this:

         Max X: 32000
         Max Y: 20000
  Max pressure: 2047
    Resolution: 4000

