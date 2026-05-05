# Architecture

The waveforms are generated digitally on the PS. The PS uploads 16-bit DAC samples into FPGA BRAM through a memory-mapped PYNQ interface. During playback, the PL streams those samples from BRAM into the RFDC, which produces the analog RF output for the amplifier and EOM.

## Overlay Datapath

The main components of the FPGA design are:

- AXI interconnect
- AXI BRAM Controller
- on-chip BRAM
- custom `DACRAMstreamer` IP
- AXI4-Stream clocking, width-conversion, and pipeline blocks
- RFDC DAC AXI4-Stream input

The BRAM is exposed to software as a memory-mapped address range. In PYNQ, that range is accessed through an MMIO-backed overlay object such as `ol.dac_player`:

```python
ol.dac_player[:] = np.int16(signal)
```

During playback, `DACRAMstreamer` reads samples sequentially from BRAM, packs the 16-bit values into wide AXI4-Stream words, and sends them through the stream infrastructure into the RFDC DAC.

## RFDC and Clocking

The implemented DAC path uses real-valued output, no interpolation, 16-bit samples, and 16 samples per AXI4-Stream cycle. That corresponds to 256 bits of sample data per stream cycle.

The physical DAC sampling rate is set by the RFDC tile clocking, not directly by the AXI clock. The RFDC tiles receive reference clocks from the board LMK/LMX clocking chain, and the RFDC tile PLL generates the high-speed DAC sampling clock. The AXI clock must still match the data rate required by the selected RFDC configuration.

When changing the DAC sampling rate, update both sides consistently:

- the RFDC configuration in Vivado
- the required AXI stream clock
- the external/reference clock and PLL setup

## Waveform Generation

Waveforms are generated on the PS with NumPy. The DAC sampling rate defines the time grid:

```text
dt = 1 / Sr
t[n] = n * dt
```

For serrodyne waveforms, the full array is split into contiguous segments. Each segment can have its own slope/frequency, phase evolution, amplitude, and sawtooth width. Segment lengths are derived from user-defined ratios, then concatenated into one waveform before upload.

## Key Takeaways

- The PS generates and uploads waveforms.
- The PL provides deterministic BRAM-to-DAC playback.
- `DACRAMstreamer` converts BRAM contents into AXI4-Stream data.
- RFDC clocking and AXI stream timing must match the intended DAC sampling rate.
