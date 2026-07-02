# Installation Guide

This page explains how to get the project running on the RFSoC 4x2 board.

![RFSoc](images/rfsoc%20board.png)

We are not going much into detail on how to get the RFSoC setup, please check out https://www.rfsoc-pynq.io/getting_started.html for that.
All infos:

- what you need to set up the RFSoC (SDcard, ethernet cable, etc..)
- how to write your image (download image from https://www.pynq.io/boards.html)
- use someting like balenaEtcher to write your image to an sdcard (https://etcher.balena.io/)
- boot up board and connect for the first time (you often see the IP addres on the oled display)
- if in doubt, use the references, they provided pretty good starting material

## 1) SSH into the board as the xilinx user

```bash
ssh xilinx@<board-ip>
```

The PYNQ Jupyter server runs as the `xilinx` user. The install script must
also run as `xilinx` — if run as root, all files land in `/root` where the
Jupyter server cannot find them and the script will refuse to continue.

> **Note**
> Do **not** run the install script from the terminal inside JupyterLab.
> The JupyterLab terminal can have a different environment and working
> directory than an SSH session, which causes the install to fail or place
> files in the wrong location. Always use a regular SSH connection.

## 2) Clone the repository and run the install script

```bash
git clone https://github.com/selfoluap/RFSoC4x2-AWG.git
cd RFSoC4x2-AWG
bash scripts/install.sh
```

This installs the `firmware` package, delivers the example notebooks via
`pynq get-notebooks`, and copies the overlay bitstream to the notebook
directory. After it finishes, the notebooks in JupyterLab can import the
overlay controller directly:

```python
from firmware import OverlayController
```

The project uses several services and tools that need board-level setup. Most prerequisites are handled by `scripts/prepare_env.sh`.

Before running it, review the script content to confirm you are comfortable with the environment changes it applies.

> **Note**
> Some hardware-related steps require elevated permissions on the RFSoC board.
