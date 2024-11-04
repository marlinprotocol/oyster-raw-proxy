![Marlin Oyster Logo](./logo.svg)

# Archival

Archived in favour of https://github.com/marlinprotocol/oyster-monorepo

# Raw Proxies

This repository contains raw IP proxies used to tunnel IP traffic through a vsock interface. They are primarily used in the tuna family of images. This repository contains the following proxies:
- ip-to-vsock-raw-incoming
- ip-to-vsock-raw-outgoing
- vsock-to-ip-raw-incoming
- vsock-to-ip-raw-outgoing

## Build

```bash
cargo build --release
```

### Reproducible builds

Reproducible builds can be done using a Rust Docker image to standardize the build environment:

```bash
# For amd64
docker run --rm -v `pwd`:/code rust@sha256:ed7795c6eaccae53be35939e883e8c3de0197b21e8eddbd9f04b0c4bc757c094 /code/build-amd64.sh

# For arm64
docker run --rm -v `pwd`:/code rust@sha256:c428882ff081342a9661fb13a1d059ecdc0b6e979ffec64b80371cf20a2088b0 /code/build-arm64.sh
```

The prebuilt binaries are then compressed using `upx` version 4.2.4. Expected sha256 checksums are available along with the links to the prebuilt binaries

## ip-to-vsock-raw-incoming

The ip-to-vsock-raw-incoming proxy listens on a netfilter queue for raw packets and proxies them to a fixed vsock address. Meant to be used in conjunction with [vsock-to-ip-raw-incoming](#vsock-to-ip-raw-incoming) proxy and iptables rules to intercept packets and redirect them into a netfilter queue.

### Prebuilt binaries

amd64: https://artifacts.marlin.org/oyster/binaries/ip-to-vsock-raw-incoming_v1.0.0_linux_amd64 \
checksum: 376d1968b12dabb81935330323177d95c04e238b5085587cb2208a820c8eaa22

arm64: https://artifacts.marlin.org/oyster/binaries/ip-to-vsock-raw-incoming_v1.0.0_linux_arm64 \
checksum: aa16d83f629a3f507dda027db96bd6493b11ae041c2f61c97fef8fff98130f05

### Usage

```bash
$ ./target/release/ip-to-vsock-raw-incoming --help
Usage: ip-to-vsock-raw-incoming --vsock-addr <VSOCK_ADDR> --queue-num <QUEUE_NUM>

Options:
  -v, --vsock-addr <VSOCK_ADDR>  vsock address to forward packets to <cid:port>
  -q, --queue-num <QUEUE_NUM>    nfqueue number of the listener <num>
  -h, --help                     Print help
  -V, --version                  Print version
```

## vsock-to-ip-raw-incoming

The vsock-to-ip-raw-incoming proxy listens on a vsock address for raw packets and proxies them to a fixed network device. Meant to be used in conjunction with [ip-to-vsock-raw-incoming](#ip-to-vsock-raw-incoming) proxy to receive raw packets.

### Prebuilt binaries

amd64: https://artifacts.marlin.org/oyster/binaries/vsock-to-ip-raw-incoming_v1.0.0_linux_amd64 \
checksum: 5bd7433956269cea0c92ca64b1e6abe5f763a3cad9c1011885a944cbc0ec53ee

arm64: https://artifacts.marlin.org/oyster/binaries/vsock-to-ip-raw-incoming_v1.0.0_linux_arm64 \
checksum: 71710819e0ef4b2032f58a02501665f636bacacb8d3f42827229da8851cc44aa

### Usage

```bash
$ ./target/release/vsock-to-ip-raw-incoming --help
Usage: vsock-to-ip-raw-incoming --vsock-addr <VSOCK_ADDR> --device <DEVICE>

Options:
  -v, --vsock-addr <VSOCK_ADDR>  vsock address to listen on <cid:port>
  -d, --device <DEVICE>          network device to forward packets on
  -h, --help                     Print help
  -V, --version                  Print version
```

## ip-to-vsock-raw-outgoing

The ip-to-vsock-raw-outgoing proxy listens on a netfilter queue for raw packets and proxies them to a fixed vsock address. Meant to be used in conjunction with [vsock-to-ip-raw-outgoing](#vsock-to-ip-raw-outgoing) proxy and iptables rules to intercept packets and redirect them into a netfilter queue.

### Prebuilt binaries

amd64: https://artifacts.marlin.org/oyster/binaries/ip-to-vsock-raw-outgoing_v1.0.0_linux_amd64 \
checksum: e94c516dd9608fe2eb2d6d6ff0be54a8f25de4cacdb289999d07bffa75364afe

arm64: https://artifacts.marlin.org/oyster/binaries/ip-to-vsock-raw-outgoing_v1.0.0_linux_arm64 \
checksum: 2f1a2f23f3157739af43735019c85bca083f05a74117102c327ca28db6c7d03f

### Usage

```bash
$ ./target/release/ip-to-vsock-raw-outgoing --help
Usage: ip-to-vsock-raw-outgoing --vsock-addr <VSOCK_ADDR> --queue-num <QUEUE_NUM>

Options:
  -v, --vsock-addr <VSOCK_ADDR>  vsock address to forward packets to <cid:port>
  -q, --queue-num <QUEUE_NUM>    nfqueue number of the listener <num>
  -h, --help                     Print help
  -V, --version                  Print version
```

## vsock-to-ip-raw-outgoing

The vsock-to-ip-raw-outgoing proxy listens on a vsock address for raw packets and proxies them to a fixed network device. Meant to be used in conjunction with [ip-to-vsock-raw-outgoing](#ip-to-vsock-raw-outgoing) proxy to receive raw packets.

### Prebuilt binaries

amd64: https://artifacts.marlin.org/oyster/binaries/vsock-to-ip-raw-outgoing_v1.0.0_linux_amd64 \
checksum: 72abb0de36ea71a7d20537bafe5166e3012537ed15930b6db0493e833e0d339f

arm64: https://artifacts.marlin.org/oyster/binaries/vsock-to-ip-raw-outgoing_v1.0.0_linux_arm64 \
checksum: 407a0949be97fd832d57da522b4868abd66ff4d2b188d204eb43979c096fb658

### Usage

```bash
$ ./target/release/vsock-to-ip-raw-outgoing --help
Usage: vsock-to-ip-raw-outgoing --vsock-addr <VSOCK_ADDR>

Options:
  -v, --vsock-addr <VSOCK_ADDR>  vsock address to listen on <cid:port>
  -h, --help                     Print help
  -V, --version                  Print version
```
