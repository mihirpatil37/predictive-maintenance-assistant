# Progress log

Task-based log: work is done in short blocks whenever time allows, so there is no fixed daily schedule. Each block ends with a commit.

## Status

| Block | Task | Status |
|---|---|---|
| 1 | Repo, venv, C-MAPSS FD001 loaded, first plot | Done (2026-10-29) |
| A | Unbox ESP32, identify USB chip, install driver | Done (2026-10-30) |
| B | Flash MicroPython with Thonny | Done (2026-10-30) |
| C | Blink LED, measure 3V3 and 5V with multimeter | In progress |
| D | Read DHT11 on the breadboard, commit script | Not started |
| E | Solder MPU-6050 headers, scan I2C for address `0x68` | Not started |
| F | Baseline RUL model on C-MAPSS FD001 | Not started |

## Log

### Block 1: data exploration (2026-10-29)
- Created the repo, a virtual environment and the notebook `notebooks/01_explore.ipynb`.
- FD001 loaded: 20,631 rows, 26 columns, 100 engines.
- Engine lifetimes range from 128 to 362 cycles (mean about 206, median 199).
- Saved the first figure: `docs/sensor11_degradation.png`.
- Lesson: the notebook ran on the global Python 3.14 instead of the project `.venv`, so pandas was "missing". Fixed by selecting the `.venv` kernel in VS Code. Packages are installed from the terminal with `python -m pip`, never from notebook cells.

### Block A: hardware identification (2026-10-30)
- Board: ESP32-WROOM-32 dev board from the LAFVIN kit, Micro-USB.
- USB chip: CP2102. Windows listed it as "CP2102 USB to UART Bridge Controller" with a warning icon under *Other devices*, meaning the driver was missing.
- COM3 and COM4 were Bluetooth serial ports and unrelated to the board.
- Installed the Silicon Labs CP210x driver, and the board then appeared under *Ports (COM & LPT)*.

### Block B: MicroPython (2026-10-30)
- Flashed MicroPython v1.29.0 (Generic ESP32 module) with Thonny's installer.
- Thonny printed "Device is busy or does not respond" once while the board was rebooting after the flash. It connected on its own afterwards.
- Verified in the shell: `print("Hello World")` returned `Hello World`.

### Block C: blink and measurements (in progress)
- [ ] `firmware/blink.py` runs: LED blinks (onboard LED on GPIO 2, or external LED on GPIO 4)
- [ ] 3V3 pin measured with multimeter: ___ V
- [ ] 5V / VIN pin measured on USB power: ___ V

## Next up
1. Finish Block C and record the real measurements above.
2. Block D: wire the DHT11 and print readings every 2 seconds.
3. Block E: MPU-6050 needs header pins soldered on before it can go on the breadboard.