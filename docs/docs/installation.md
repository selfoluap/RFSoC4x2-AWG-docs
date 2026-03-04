# Installation Guide

This page explains how to get the project running on the RFSoC 4x2 board.

![RFSoc](images/rfsoc%20board.png)

We are not going much into detail on how to get the RFSoC setup, please check out https://www.rfsoc-pynq.io/getting_started.html for that.

## 1) Clone the repository

```bash
git clone https://github.com/selfoluap/RFSoC4x2-AWG.git
cd RFSoC4x2-AWG
```

## 2) Run install script

```bash
source scripts/prepare_env.sh
```

The project uses several services and tools that need board-level setup. Most prerequisites are handled by `scripts/prepare_env.sh`.

Before running it, review the script content to confirm you are comfortable with the environment changes it applies.

> **Note**
> Some hardware-related steps require elevated permissions on the RFSoC board.
