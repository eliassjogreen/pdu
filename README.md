# 10" 1U PDU

A modular 10" 1U PDU which repurposes the common slot HP server power supplies.
It's designed around a single 12V rail supplied by the powerful and probably
overkill HP common slot power supplies. To supply downstream devices there are
internal XT60 connectors, which in turn are used to buck or boost the 12V rail
to desired voltages, for example 19V for common mini-pc's.

## Specifications

Depending on the [HP common slot power supply](https://support.hpe.com/hpesc/public/docDisplay?docId=c03502743)
you decide to get there is some variation in the capabilities of the PDU. I
have the 750W (DPS-750RB and HSTNS-PL18) variant of the supply outputting 12V
62.5A on the main rail, but also 12V 2.5A of standby power which is always on.
The PDU will probably work with the 1200W version, but because I designed it
with the 750W version in mind some connectors and the PCB might technically be
undersized for such loads. The smaller 460W version should work just fine still.

There are 6 XT60 connectors on the rail for supplying different devices,
supporting 30A continuous current and 60A surge current each, which should
be more than enough for most devices (360W 12V). The main bottleneck will be
the jumper module which connects the PSU to the rail (and in the future a
backup PSU or UPS), which is currently designed arount the XT90 connector which
is "only" rated for 45A continuous current and 90A surge current which may be a
problem if you draw >540W continuously from the rail. For most homelabs this
shouldn't be any issue though, and if it is I sincerely wonder what you managed
to cram into a 10" rack?!

## Progress

Currently there's only a backplane and a simple jumper module which connects
the PSU's 12V main output to the rail, but I am planning on adding a
ideal-diode/power path controller for connecting a second power supply or
external UPS I am planning on building.

Additionally there will be USB PD modules, hopefully supporting 144W devices.
The possibilites are endless, maybe even 48V for PoE devices, but I don't
currently have any so that will have to wait.

The controller will probably (not decided yet) use a RP2040 or compatible
microcontroller with some yet-to-be-coded firmware which probably will
interface with [USB HID](https://www.usb.org/sites/default/files/pdcv11.pdf)
for power devices for interfacing with [NUT](https://networkupstools.org/).
This is still very much in the planning phase and nothing is decided yet, and
probably will be way simpler for the first revision.

## Licenses

### Hardware

All hardware including but not limited to: PCB layouts, schematics, CAD files,
BOM, gerbers, graphic designs and hardware documentation are licensed under the
CERN-OHL-S-V2 license as found [here](LICENSES/CERN-OHL-S-2.0.txt).

### Software

All software including but not limited to: firmware, scripts, configuration
files and software documentation are licensed under the GPLv3 license as found
[here](LICENSES/GPL-3.0.txt).
