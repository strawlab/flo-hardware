### 2core_150hz.uf2

repo "flo", commit f09567209f743149737f25a288ec7477a84578f4 "BYO version (set framerate to 150)" from 2024-01-08

* 150 fps
* lowest latency and jitter (~0.5us)
* servo pan-tilt support
* no helpful led indication

### triggerbox3_150hz.uf2

repo "triggerbox3", commit 5642ef4baf671fd3158a605e175da9fd28572022 "fix slight framertate inaccuracy" from 2024-01-12 with framerate changed to 150 Hz

* 150 fps
* simplest code
* helpful led indicator
* latency 1.6us

### triggerbox-byo_150Hz.uf2

repo "triggerbox", commit 2481c838a23c9e029a0b8c12ed90d987596e1336 "set default framerate to 150 fps" from 2024-01-12

* 150 fps by default
* framerate is adjustable via usb
* helpful led indicator
* latency 2.3us