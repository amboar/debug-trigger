# BMC Debug Trigger #

`debug-trigger` listens for an external signal that the BMC is in some way
unresponsive. When the signal is received it triggers a crash to collect debug
data and reboots the system in the hope that it will recover.

## Trigger sources ##

`debug-trigger` implements a simple protocol over an LPC KCS device as its
trigger source.

## Debug actions ##

`debug-trigger` implements a single action once the trigger event is received,
which is to crash the kernel via `/proc/sysrq-trigger`. For systems with kdump
configured this results in collection of system state as context for why the
system was externally unresponsive.
