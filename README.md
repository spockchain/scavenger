Scavenger can also be installed directly via cargo:

### Config
Update plot_dirs and url in config.yaml before running.

``` shell
cargo install scavenger
```

``` shell
# decide on features to run/build:
simd: support for SSE2, AVX, AVX2 and AVX512F (x86_cpu)
neon: support for Arm NEON (arm_cpu)
opencl: support for OpenCL (gpu)

# build debug und run directly
e.g. cargo run --features=simd    #for a cpu version with SIMD support

# build debug (unoptimized)
e.g cargo build --features=neon   #for a arm cpu version with NEON support

# build release (optimized)
e.g. cargo build --release --features=opencl,simd    #for a cpu/gpu version

# test
cargo test  [--features={opencl,simd,neon}]
```

### Run

```shell
scavenger --help
```

### Docker

A docker image based on alpine linux is built automatically on every commit to master: `pocconsortium/scavenger`
This image will use only your cpu.

To run it on the fly use something like this:
```
docker run \
--rm \
--name scavenger \
--volume /path/to/your/config.yaml:/data/config.yaml \
--volume /path/to/your/disks:/disks \
pocconsortium/scavenger
```

Alternatively a docker compose file could look like this:
```
version: '2'
services:
  scavenger:
    image: pocconsortium/scavenger
    restart: always
    volumes:
      - /path/to/your/disks:/disks
      - /path/to/your/config.yaml:/data/config.yaml
```
