so how does it work

we generate signal spaced out over tota length of BRAM

BRAM has width of xxx bit and in address editor in viado we define general size of BRAM
based on these BRAM size, we

from ZYNY IP
used to write data over AXI to shared memory space
in python via MMIO class, set start address and range exactly as specified in address editor

high performance axi port to axi intreconnect

data is 16 bit ints
data gets forwarded to AXI bram controller and block memory

we then stream at
