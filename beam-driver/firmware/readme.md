# Firmware binary

This file can be flashed onto the Raspberry Pi Pico onboard the Dual Cam PCB.
Hold the boot button while plugging in the Raspberry Pi Pico to your PC. This
will bring it up as a USB Mass Storage device onto which you can drag and drop
the `.uf2` file here.

### beamdriver-150Hz.uf2

Source code: [repo "flo", commit c64758fc95ba7cb73e0c1d8a02bef2db8ca351d4 "Merge branch 'firmware-beamdriver'"](https://github.com/strawlab/flo/tree/c64758fc95ba7cb73e0c1d8a02bef2db8ca351d4/firmware/beamdriver)

Characteristics:
* 150 fps
* lowest latency and jitter (~0.5us)
* no helpful led indication
