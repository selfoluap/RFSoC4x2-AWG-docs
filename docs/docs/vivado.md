# Modifying the Vivado Overlay

Here you can find instructions if you want to modify the overlay.

## Links

https://www.xilinx.com/support/download.html for downloading Vivado

## Prerequisites

- Vivado Design Suite 2022.1
- RFSoC 4x2 Board Files installed in Vivado
- A valid Vivado license (node-locked or floating via FlexNet/lmgrd)

Use the provided Tcl script to regenerate the project.

For convenience, there are helper scripts for the common development workflow. After successful bitstream generation, they collect the required `.bit` and `.hwh` files and can push them to the RFSoC over SSH.

In the original setup, deployment was done over Tailscale using a hostname. If you are not using Tailscale, replace the hostname with your board IP (see `networking.md`).

## Practical Notes

- If you only need to **use** an existing overlay, you do not need to rebuild Vivado projects. Use the prebuilt overlays in the `overlays/` directory.
- Overlay builds can take a long time depending on your machine and design state; expect roughly **20–60 minutes** per full build.
- The exported Tcl was generated from Vivado GUI using `write_tcl`; regeneration may require small environment-specific fixes.
