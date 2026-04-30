# RFSoC AWG

This project implements an AWG on the Xilinx RFSoC 4x2 development board. It was developed in the LaserLab Group at Vrije Universiteit Amsterdam to support laser cooling experiments.

## Architecture Overview

We use a hybrid approach where the CPU generates the waveform, while the FPGA outputs it.

![Zynq Architecture](images/zynq.png)

For more information on the board, please refer to [Additional resources](board.md)

## Quick Start

I would start with installation first. Get your board ready and also get a bit accusted to the board. Do some of the loopback experiments that are provided. I

1. [Install the software](installation.md)
2. [Configure networking](networking.md)
3. [Set up remote access](tailscale.md)
