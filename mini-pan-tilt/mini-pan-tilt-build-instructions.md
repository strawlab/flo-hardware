### Bill of Materials
#### Mechanical parts

- 1x Lynxmotion: Lynx B - Pand and Tilt Kit (Black Anodized), inluding:
	- 1x Aluminum Multi-Purpose Servo Bracket Single (ASB-04)
	- 1x Auminum "C" Servo Bracket Single (ASB-03)
	- 2x HS-422 standard servo (S422)
	- Hardware (in particular: 4x small black screws for servos, 1x black M1 screw with washer and nut for tilt axis, nylon rivets)
		this seems to be the newer version:
		https://www.robotshop.com/products/lynxmotion-pan-and-tilt-kit-aluminium2
		
- 1x Thorlabs base plate 150x150x12.7 mm, M6 Taps (I think it's the right one)
		https://www.thorlabs.de/thorproduct.cfm?partnumber=MB1515/M
- 1x M6 hex screw
- 1x custom 3D printed support bracket (include file)
- 4x M3x20 hex screws + nuts
- SCube Basler Tripod Adapter:
	- Base Plate
	- 4x M2 x 5 hex cap screws
- 1x 1/4"-20  3/8" cap screw + 2x washers (or shorter screw)

#### Electronics
	
- Raspberry Pi Pico (RP2040 based) microcontroller
- pin headers .1

#### Optical

- Basler .... camera
- CS-mount lens: 16mm 1:1.6 1/3"  IR


### Hardware build instruction

#### Pan-Tilt-Assembly

1. Mount Camera on "C" Bracket:
	1. Attatch SCube Basler Tripod adapter to base of camera using M2 x 20 cap screws
	2. Attatch "C" Bracket to Adapter using 1/4"-20  3/8" cap screw  and washers
2. Assemble Pan-Tilt-Setup
	1. for each servo motor, replace the preinstalled "arm" with the disk shaped one:
		- turn the servo all the way counter-clockwise
		- remove arm
		- mount disk with '1' in the top position
	1. Mount Multi-Purpose Servo Bracket to Pan-servo
		- turn disk unitl '2' is in the top position
		- attatch Multi-Puropse bracket in parallel with the servo. Use small balck screws to attatch bracket to disk
	2. Mount Tilt-servo
		- attatch one side of "C" bracket (with mounted camera) to the multi-purpose backet
		- mount tilt-servo to multi-purpose bracket using nylon rivets
		- turn disk on tilt-servo to have '3' in top postition
		- attach loose end of "C" bracket  to disk. Make sure that the disk is in the right position!
	3. Mount on base plate
		 - Attatch 3D printed support bracket to base plate with M6 screw
		 - attatch pan-servo to support bracket using M3 x 20 screws and nuts
	4. Mount desired lens on camera

#### Connecting the Raspberry Pi Pico



30 (run) - s0
29 - s1



### Ethernet Basler Setup

PoE power injector
pyhon ip configurator
mac - address 

make sure it gets ip addr

### Software & firmware installation

#### 1. Rust installation and configuration


#### 2. Flo installation

Now using the `gimbal` branch as it seems to be the most current one

```bash
git clone https://gitlab.strawlab.org/straw/flo.git
git fetch origin gimbal
git switch gimbal
```

if necessary, rebuild `flo-bui`
```shell
cd flo-bui
./build.sh
```
#### 3. Flashing firmware: PanTilt for RP-pico - Receive from USB (serial) and emit PWM for two servos

Firmware for the Raspberry Pi Pico is located in `./flo/rpipico-pantilt/`
These instructions are based on the [Readme.md](https://gitlab.strawlab.org/straw/flo/-/blob/stereopsis/rpipico-pantilt/README.md), which in turn are based on [rp2040-project-template](https://github.com/rp-rs/rp2040-project-template). 
##### Installation of development dependencies


```sh

rustup target install thumbv6m-none-eabi

cargo install flip-link

# This is our suggested default 'runner', we are not using this runner

cargo install probe-run

# If you want to use elf2uf2-rs instead of probe-run, instead do...
# That's what we are doing

cargo install elf2uf2-rs --locked

```
##### Running: We are going to load a UF2 over USB

 _Step 1_ -  Modify `.cargo/config` to change the default runner to
  
  ```
[target.`cfg(all(target-arch = "arm", target_os = "none"))`]
# runner = "probe-run --chip RP2024"
runner = "elf2uf2-rs -d"
```

_Step 2_ - Boot RP2040 into "USB Bootloader mode". Keep "BOOTSEL" button pressed while connecting to the PC. It should now be mounted in 'Flash drive mode.

_Step 3_ - Use `cargo run`, which will compile the code and start the specified 'runner'. As the 'runner' is the `elf2uf2-rs` tool, it will build a UF2 file and copy it to your RP2040.

For a debug build
```sh
cargo run
```

For a release build
```shell
cargo run --release
```


