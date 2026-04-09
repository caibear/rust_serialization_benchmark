<!-- AUTOMATICALLY GENERATED, DO NOT EDIT -->
<!-- edit README.md.template instead -->

# Rust serialization benchmark

The goal of these benchmarks is to provide thorough and complete benchmarks for various rust
serialization frameworks.

## Maintainers

These benchmarks are maintained by a small group of volunteers. Special thanks to:

- [djkoloski](https://github.com/djkoloski)
- [mumbleskates](https://github.com/mumbleskates)
- [finnbear](https://github.com/finnbear)

## These benchmarks are a work in progress

These benchmarks are still being developed and pull requests to improve benchmarks are welcome.

## [Interactive site](https://djkoloski.github.io/rust_serialization_benchmark/)

Calculate the number of messages per second that can be sent/received with various rust serialization frameworks and compression libraries.
[Documentation](pages/README.md)

## Format

All tests benchmark the following properties (time or size):

* **Serialize**: serialize data into a buffer
* **Deserialize**: deserializes a buffer into a normal rust object
* **Borrow**: deserializes a buffer into a rust object that borrows string data from the input, with lifetime
* **Size**: the size of the buffer when serialized
* **Zlib**: the size of the buffer after zlib compression
* **Zstd**: the size of the buffer after zstd compression
* **Zstd Time**: the time taken to compress the serialized buffer with zstd

Zero-copy deserialization libraries have an additional set of benchmarks:

* **Access**: accesses a buffer as structured data
* **Read**: runs through a buffer and reads fields out of it
* **Update**: updates a buffer as structured data

Some benchmark results may be italicized and followed by an asterisk. Mouse over these for more details on what situation was benchmarked. Other footnotes are located at the bottom.

## Last updated: 2026-04-09 00:05:40

<details><summary>Runtime info</summary>

### `rustc` version

```
rustc 1.96.0-nightly (c75612477 2026-04-07)
binary: rustc
commit-hash: c756124775121dea0e640652c5ee3c89e3dd0eb4
commit-date: 2026-04-07
host: x86_64-unknown-linux-gnu
release: 1.96.0-nightly
LLVM version: 22.1.2
```

### CPU info

```
Architecture:                            x86_64
CPU op-mode(s):                          32-bit, 64-bit
Address sizes:                           48 bits physical, 48 bits virtual
Byte Order:                              Little Endian
CPU(s):                                  4
On-line CPU(s) list:                     0-3
Vendor ID:                               AuthenticAMD
Model name:                              AMD EPYC 7763 64-Core Processor
CPU family:                              25
Model:                                   1
Thread(s) per core:                      2
Core(s) per socket:                      2
Socket(s):                               1
Stepping:                                1
BogoMIPS:                                4890.84
Flags:                                   fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl tsc_reliable nonstop_tsc cpuid extd_apicid aperfmperf tsc_known_freq pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand hypervisor lahf_lm cmp_legacy svm cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw topoext vmmcall fsgsbase bmi1 avx2 smep bmi2 erms invpcid rdseed adx smap clflushopt clwb sha_ni xsaveopt xsavec xgetbv1 xsaves user_shstk clzero xsaveerptr rdpru arat npt nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold v_vmsave_vmload umip vaes vpclmulqdq rdpid fsrm
Virtualization:                          AMD-V
Hypervisor vendor:                       Microsoft
Virtualization type:                     full
L1d cache:                               64 KiB (2 instances)
L1i cache:                               64 KiB (2 instances)
L2 cache:                                1 MiB (2 instances)
L3 cache:                                32 MiB (1 instance)
NUMA node(s):                            1
NUMA node0 CPU(s):                       0-3
Vulnerability Gather data sampling:      Not affected
Vulnerability Ghostwrite:                Not affected
Vulnerability Indirect target selection: Not affected
Vulnerability Itlb multihit:             Not affected
Vulnerability L1tf:                      Not affected
Vulnerability Mds:                       Not affected
Vulnerability Meltdown:                  Not affected
Vulnerability Mmio stale data:           Not affected
Vulnerability Old microcode:             Not affected
Vulnerability Reg file data sampling:    Not affected
Vulnerability Retbleed:                  Not affected
Vulnerability Spec rstack overflow:      Vulnerable: Safe RET, no microcode
Vulnerability Spec store bypass:         Vulnerable
Vulnerability Spectre v1:                Mitigation; usercopy/swapgs barriers and __user pointer sanitization
Vulnerability Spectre v2:                Mitigation; Retpolines; STIBP disabled; RSB filling; PBRSB-eIBRS Not affected; BHI Not affected
Vulnerability Srbds:                     Not affected
Vulnerability Tsa:                       Vulnerable: No microcode
Vulnerability Tsx async abort:           Not affected
Vulnerability Vmscape:                   Not affected
```

</details>

## `log`

This data set is composed of HTTP request logs that are small and contain many strings.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Borrow | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*433.42 µs\**</span> <span title="prepend">*420.34 µs\**</span> | 2.5298 ms | 885.57 µs | 804955 | 328941 | 284849 | 4.1304 ms |
| [bin-proto 0.12.3][bin-proto] | 4.6079 ms | 4.7604 ms | † | 1045784 | 373127 | 311553 | 4.5187 ms |
| [bincode 2.0.1][bincode] | 328.54 µs | 2.1356 ms | 694.09 µs | 741295 | 303944 | 256422 | 3.6837 ms |
| [bincode 1.3.3][bincode1] | 551.71 µs | 2.7523 ms | 616.05 µs | 1045784 | 373127 | 311553 | 4.4599 ms |
| [bitcode 0.6.6][bitcode] | 145.22 µs | 1.4564 ms | 62.563 µs | 703710 | 288826 | 227322 | 2.5261 ms |
| [borsh 1.5.7][borsh] | 550.47 µs | 2.1360 ms | † | 885780 | 362204 | 286248 | 4.0922 ms |
| [capnp 0.23.2][capnp] | 464.78 µs | † | † | 1443216 | 513986 | 426532 | 6.1901 ms |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 618.52 µs | 5.1296 ms | 3.3507 ms | 1407835 | 403440 | 323561 | 5.0481 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 3.2691 ms | 11.393 ms | † | 1407835 | 403440 | 323561 | 4.9784 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 1.9244 ms | 4.9222 ms | 3.1239 ms | 1407835 | 403440 | 323561 | 5.1397 ms |
| [columnar 0.11.1][columnar] | 256.34 µs | 2.1941 ms <span title="copy_from">*829.21 µs\**</span> | † | 1045928 | 370212 | 293907 | 4.1760 ms |
| [databuf 0.5.0][databuf] | 280.03 µs | 2.0389 ms | 668.41 µs | 765778 | 311715 | 263914 | 3.4740 ms |
| [dlhn 0.1.7][dlhn] | 636.15 µs | 2.6150 ms | † | 724953 | 301446 | 253056 | 3.1948 ms |
| [flatbuffers 25.12.19][flatbuffers] | 1.0473 ms | † | † | 1276368 | 468539 | 388381 | 4.7218 ms |
| [flexbuffers 25.2.10][flexbuffers] | 6.6774 ms | 7.6603 ms | 6.0280 ms | 1829756 | 714318 | 691541 | 8.5148 ms |
| json:<br> [flexon 0.4.5][flexon] | 2.7648 ms | 3.9286 ms | † | 1827461 | 470560 | 360727 | 5.5402 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 4.2541 ms | 5.9069 ms | † | 1827461 | 470560 | 360727 | 5.9502 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 2.1679 ms | 4.7915 ms | † | 1827461 | 470560 | 360727 | 5.4905 ms |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 935.46 µs | 2.6076 ms | † | 764996 | 315291 | 264212 | 3.7864 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 1.4213 ms | 3.1618 ms | 1.3914 ms | 784997 | 325384 | 277608 | 3.8416 ms |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 380.89 µs | 2.4443 ms | 803.45 µs | 784997 | 325384 | 277608 | 3.7633 ms |
| [minicbor 1.0.0][minicbor] | 701.58 µs | 3.0144 ms | 1.4127 ms | 817830 | 332671 | 284034 | 4.0406 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 5.5645 ms | 4.1054 ms | 2.4859 ms | 818669 | 332556 | 284797 | 4.2984 ms |
| [nanoserde 0.2.1][nanoserde] | 260.05 µs | 2.0970 ms | † | 1045784 | 373127 | 311553 | 4.2157 ms |
| [nibblecode 0.1.0][nibblecode] | 193.10 µs | † | † | 1011487 | 473180 | 403991 | 5.6232 ms |
| [postcard 1.1.1][postcard] | 423.75 µs | 2.2872 ms | 707.76 µs | 724953 | 302399 | 252968 | 3.4491 ms |
| [pot 3.0.1][pot] | 2.3316 ms | 6.4594 ms | 4.8477 ms | 971922 | 372513 | 303636 | 4.3853 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*942.62 µs\**</span> <span title="populate + encode">*2.4449 ms\**</span> | 3.2828 ms | † | 884628 | 363130 | 314959 | 4.3454 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*1.1958 ms\**</span> <span title="populate + encode">*2.9994 ms\**</span> | 3.8192 ms | † | 884628 | 363130 | 314959 | 4.3488 ms |
| [rkyv 0.8.10][rkyv] | 239.28 µs | <span title="unvalidated">*1.5390 ms\**</span> <span title="validated upfront with error">*1.8904 ms\**</span> | † | 1011488 | 393526 | 325965 | 4.6574 ms |
| [ron 0.10.1][ron] | 12.244 ms | 24.785 ms | 22.915 ms | 1607459 | 449158 | 349324 | 5.5436 ms |
| [savefile 0.18.6][savefile] | 197.16 µs | 2.0576 ms | † | 1045800 | 373139 | 311562 | 4.1697 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 672.26 µs | 2.4039 ms | † | 765778 | 311743 | 263822 | 3.7942 ms |
| [serde-brief 0.1.1][serde-brief] | 1.3952 ms | 4.6668 ms | 2.9620 ms | 1584946 | 413733 | 339964 | 4.8856 ms |
| [serde_bare 0.5.0][serde_bare] | 693.17 µs | 2.0909 ms | † | 765778 | 311715 | 263914 | 3.5227 ms |
| [speedy 0.8.7][speedy] | 200.40 µs | 1.7652 ms | 366.79 µs | 885780 | 362204 | 286248 | 3.8648 ms |
| [wincode 0.2.4][wincode] | 179.53 µs | 1.9599 ms | 500.89 µs | 1045784 | 373127 | 311553 | 4.1735 ms |
| [wiring 0.2.4][wiring] | 194.86 µs | 2.0839 ms | † | 1045784 | 337930 | 275808 | 3.6370 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*81.037 ns\**</span> | <span title="validated on-demand with error">*132.47 µs\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 23.039 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.4896 ns\**</span> <span title="validated upfront with error">*2.1326 ms\**</span> | <span title="unvalidated">*49.431 µs\**</span> <span title="validated upfront with error">*2.1729 ms\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.2448 ns\**</span> <span title="validated upfront with error">*245.55 µs\**</span> | <span title="unvalidated">*10.394 µs\**</span> <span title="validated upfront with error">*256.31 µs\**</span> | <span title="unvalidated">*9.0199 µs\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.2455 ns\**</span> <span title="validated upfront with error">*338.04 µs\**</span> | <span title="unvalidated">*10.417 µs\**</span> <span title="validated upfront with error">*346.36 µs\**</span> | <span title="unvalidated">*7.4976 µs\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Borrow | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*33.51%\**</span> <span title="prepend">*34.55%\**</span> | 32.78% | 7.06% | 87.42% | 87.80% | 79.80% | 61.16% |
| [bin-proto 0.12.3][bin-proto] | 3.15% | 17.42% | † | 67.29% | 77.41% | 72.96% | 55.90% |
| [bincode 2.0.1][bincode] | 44.20% | 38.83% | 9.01% | 94.93% | 95.03% | 88.65% | 68.58% |
| [bincode 1.3.3][bincode1] | 26.32% | 30.13% | 10.16% | 67.29% | 77.41% | 72.96% | 56.64% |
| [bitcode 0.6.6][bitcode] | 100.00% | 56.94% | 100.00% | 100.00% | 100.00% | 100.00% | 100.00% |
| [borsh 1.5.7][borsh] | 26.38% | 38.82% | † | 79.45% | 79.74% | 79.41% | 61.73% |
| [capnp 0.23.2][capnp] | 31.24% | † | † | 48.76% | 56.19% | 53.30% | 40.81% |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 23.48% | 16.17% | 1.87% | 49.99% | 71.59% | 70.26% | 50.04% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 4.44% | 7.28% | † | 49.99% | 71.59% | 70.26% | 50.74% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 7.55% | 16.85% | 2.00% | 49.99% | 71.59% | 70.26% | 49.15% |
| [columnar 0.11.1][columnar] | 56.65% | 37.79% <span title="copy_from">*100.00%\**</span> | † | 67.28% | 78.02% | 77.34% | 60.49% |
| [databuf 0.5.0][databuf] | 51.86% | 40.67% | 9.36% | 91.89% | 92.66% | 86.13% | 72.71% |
| [dlhn 0.1.7][dlhn] | 22.83% | 31.71% | † | 97.07% | 95.81% | 89.83% | 79.07% |
| [flatbuffers 25.12.19][flatbuffers] | 13.87% | † | † | 55.13% | 61.64% | 58.53% | 53.50% |
| [flexbuffers 25.2.10][flexbuffers] | 2.17% | 10.82% | 1.04% | 38.46% | 40.43% | 32.87% | 29.67% |
| json:<br> [flexon 0.4.5][flexon] | 5.25% | 21.11% | † | 38.51% | 61.38% | 63.02% | 45.60% |
| json:<br> [serde_json 1.0.140][serde_json] | 3.41% | 14.04% | † | 38.51% | 61.38% | 63.02% | 42.45% |
| json:<br> [simd-json 0.15.1][simd-json] | 6.70% | 17.31% | † | 38.51% | 61.38% | 63.02% | 46.01% |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 15.52% | 31.80% | † | 91.99% | 91.61% | 86.04% | 66.72% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 10.22% | 26.23% | 4.50% | 89.64% | 88.76% | 81.89% | 65.76% |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 38.13% | 33.92% | 7.79% | 89.64% | 88.76% | 81.89% | 67.12% |
| [minicbor 1.0.0][minicbor] | 20.70% | 27.51% | 4.43% | 86.05% | 86.82% | 80.03% | 62.52% |
| [nachricht-serde 0.4.0][nachricht-serde] | 2.61% | 20.20% | 2.52% | 85.96% | 86.85% | 79.82% | 58.77% |
| [nanoserde 0.2.1][nanoserde] | 55.84% | 39.54% | † | 67.29% | 77.41% | 72.96% | 59.92% |
| [nibblecode 0.1.0][nibblecode] | 75.20% | † | † | 69.57% | 61.04% | 56.27% | 44.92% |
| [postcard 1.1.1][postcard] | 34.27% | 36.25% | 8.84% | 97.07% | 95.51% | 89.86% | 73.24% |
| [pot 3.0.1][pot] | 6.23% | 12.84% | 1.29% | 72.40% | 77.53% | 74.87% | 57.60% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*15.41%\**</span> <span title="populate + encode">*5.94%\**</span> | 25.26% | † | 79.55% | 79.54% | 72.18% | 58.13% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*12.14%\**</span> <span title="populate + encode">*4.84%\**</span> | 21.71% | † | 79.55% | 79.54% | 72.18% | 58.09% |
| [rkyv 0.8.10][rkyv] | 60.69% | <span title="unvalidated">*53.88%\**</span> <span title="validated upfront with error">*43.86%\**</span> | † | 69.57% | 73.39% | 69.74% | 54.24% |
| [ron 0.10.1][ron] | 1.19% | 3.35% | 0.27% | 43.78% | 64.30% | 65.07% | 45.57% |
| [savefile 0.18.6][savefile] | 73.66% | 40.30% | † | 67.29% | 77.40% | 72.96% | 60.58% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 21.60% | 34.49% | † | 91.89% | 92.65% | 86.16% | 66.58% |
| [serde-brief 0.1.1][serde-brief] | 10.41% | 17.77% | 2.11% | 44.40% | 69.81% | 66.87% | 51.71% |
| [serde_bare 0.5.0][serde_bare] | 20.95% | 39.66% | † | 91.89% | 92.66% | 86.13% | 71.71% |
| [speedy 0.8.7][speedy] | 72.47% | 46.98% | 17.06% | 79.45% | 79.74% | 79.41% | 65.36% |
| [wincode 0.2.4][wincode] | 80.89% | 42.31% | 12.49% | 67.29% | 77.41% | 72.96% | 60.53% |
| [wiring 0.2.4][wiring] | 74.53% | 39.79% | † | 67.29% | 85.47% | 82.42% | 69.46% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.54%\**</span> | <span title="validated on-demand with error">*7.85%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 5.40% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*50.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*21.03%\**</span> <span title="validated upfront with error">*0.48%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*4.06%\**</span> | <span title="unvalidated">*83.12%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*99.94%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*99.78%\**</span> <span title="validated upfront with error">*3.00%\**</span> | <span title="unvalidated">*100.00%\**</span> |

## `mesh`

This data set is a single mesh. The mesh contains an array of triangles, each of which has three vertices and a normal vector.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*7.3039 ms\**</span> <span title="prepend">*8.8163 ms\**</span> | 7.6955 ms | 8625005 | 6443961 | 6231572 | 75.423 ms |
| [bin-proto 0.12.3][bin-proto] | 8.7941 ms | 10.716 ms | 6000008 | 5378500 | 5346908 | 8.5424 ms |
| [bincode 2.0.1][bincode] | 2.4170 ms | 1.0366 ms | 6000005 | 5378497 | 5346882 | 8.5529 ms |
| [bincode 1.3.3][bincode1] | 5.8804 ms | 4.4243 ms | 6000008 | 5378500 | 5346908 | 8.4519 ms |
| [bitcode 0.6.6][bitcode] | 1.3012 ms | 816.57 µs | 6000006 | 5182295 | 4921841 | 13.374 ms |
| [borsh 1.5.7][borsh] | 6.2141 ms | 4.1375 ms | 6000004 | 5378496 | 5346866 | 8.5303 ms |
| [capnp 0.23.2][capnp] | 6.3554 ms | † | 14000088 | 7130367 | 6046182 | 82.751 ms |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 9.0192 ms | 49.110 ms | 13125016 | 7524114 | 6757437 | 96.878 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 67.360 ms | 125.57 ms | 13122324 | 7524660 | 6759128 | 91.780 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 35.852 ms | 41.044 ms | 13122324 | 7524660 | 6759128 | 92.873 ms |
| [columnar 0.11.1][columnar] | 1.8861 ms | 1.4205 ms <span title="copy_from">*711.34 µs\**</span> | 6000120 | 5378435 | 5347039 | 8.6235 ms |
| [databuf 0.5.0][databuf] | 2.4154 ms | 5.3723 ms | 6000003 | 5378495 | 5346897 | 8.8140 ms |
| [dlhn 0.1.7][dlhn] | 5.9674 ms | 6.8294 ms | 6000003 | 5378495 | 5346897 | 8.7962 ms |
| [flatbuffers 25.12.19][flatbuffers] | 472.63 µs | † | 6000024 | 5378434 | 5346878 | 8.9271 ms |
| [flexbuffers 25.2.10][flexbuffers] | 103.49 ms | 92.979 ms | 26609424 | 11901040 | 12486322 | 152.98 ms |
| json:<br> [flexon 0.4.5][flexon] | 76.807 ms | 57.391 ms | 26192883 | 9566084 | 8584671 | 154.97 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 90.169 ms | 98.857 ms | 26192883 | 9566084 | 8584671 | 154.93 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 54.366 ms | 66.988 ms | 26192883 | 9566084 | 8584671 | 155.05 ms |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 3.1695 ms | 4.9905 ms | 7500005 | 6058442 | 6014500 | 10.362 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 18.415 ms | 16.432 ms | 8125006 | 6494876 | 6391037 | 74.190 ms |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 732.48 µs | 5.2698 ms | 8125006 | 6494876 | 6391037 | 76.323 ms |
| [minicbor 1.0.0][minicbor] | 6.0652 ms | 11.497 ms | 8125006 | 6494907 | 6390894 | 70.388 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 120.25 ms | 29.098 ms | 8125037 | 6493484 | 6386940 | 75.733 ms |
| [nanoserde 0.2.1][nanoserde] | 1.6528 ms | 892.40 µs | 6000008 | 5378500 | 5346908 | 8.5094 ms |
| [nibblecode 0.1.0][nibblecode] | 198.68 µs | † | 6000008 | 5378500 | 5346908 | 8.6386 ms |
| [postcard 1.1.1][postcard] | 482.72 µs | 1.0142 ms | 6000003 | 5378495 | 5346897 | 8.6877 ms |
| [pot 3.0.1][pot] | 39.675 ms | 70.663 ms | 10122342 | 6814618 | 6852252 | 83.967 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*8.0129 ms\**</span> <span title="populate + encode">*8.7037 ms\**</span> | 11.026 ms | 8750000 | 6665735 | 6421877 | 72.249 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*15.528 ms\**</span> <span title="populate + encode">*31.853 ms\**</span> | 29.050 ms | 8750000 | 6665735 | 6421877 | 79.842 ms |
| [rkyv 0.8.10][rkyv] | 198.25 µs | <span title="unvalidated">*199.88 µs\**</span> <span title="validated upfront with error">*151.78 µs\**</span> | 6000008 | 5378500 | 5346872 | 8.3931 ms |
| [ron 0.10.1][ron] | 175.29 ms | 512.09 ms | 22192885 | 8970395 | 8137334 | 147.81 ms |
| [savefile 0.18.6][savefile] | 148.14 µs | 198.59 µs | 6000024 | 5378519 | 5346896 | 8.6851 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 5.1209 ms | 4.1579 ms | 6000004 | 5378496 | 5346866 | 8.5950 ms |
| [serde-brief 0.1.1][serde-brief] | 17.644 ms | 36.570 ms | 15750015 | 8024540 | 6813667 | 93.873 ms |
| [serde_bare 0.5.0][serde_bare] | 6.4819 ms | 4.6848 ms | 6000003 | 5378495 | 5346897 | 8.6721 ms |
| [speedy 0.8.7][speedy] | 199.56 µs | 151.13 µs | 6000004 | 5378496 | 5346866 | 8.5085 ms |
| [wincode 0.2.4][wincode] | 198.63 µs | 149.47 µs | 6000008 | 5378500 | 5346908 | 8.6298 ms |
| [wiring 0.2.4][wiring] | 199.03 µs | 341.55 µs | 6000008 | 5378952 | 5346905 | 8.6531 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*111.39 ns\**</span> | <span title="validated on-demand with error">*1.9739 ms\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 21.797 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.4888 ns\**</span> <span title="validated upfront with error">*44.611 ns\**</span> | <span title="unvalidated">*77.852 µs\**</span> <span title="validated upfront with error">*77.898 µs\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.2450 ns\**</span> <span title="validated upfront with error">*1.5593 ns\**</span> | <span title="unvalidated">*38.904 µs\**</span> <span title="validated upfront with error">*38.907 µs\**</span> | <span title="unvalidated">*79.190 µs\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.2448 ns\**</span> <span title="validated upfront with error">*4.8058 ns\**</span> | <span title="unvalidated">*38.902 µs\**</span> <span title="validated upfront with error">*38.935 µs\**</span> | <span title="unvalidated">*99.587 µs\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*2.03%\**</span> <span title="prepend">*1.68%\**</span> | 1.94% | 69.57% | 80.42% | 78.98% | 11.13% |
| [bin-proto 0.12.3][bin-proto] | 1.68% | 1.39% | 100.00% | 96.35% | 92.05% | 98.25% |
| [bincode 2.0.1][bincode] | 6.13% | 14.42% | 100.00% | 96.35% | 92.05% | 98.13% |
| [bincode 1.3.3][bincode1] | 2.52% | 3.38% | 100.00% | 96.35% | 92.05% | 99.30% |
| [bitcode 0.6.6][bitcode] | 11.38% | 18.30% | 100.00% | 100.00% | 100.00% | 62.76% |
| [borsh 1.5.7][borsh] | 2.38% | 3.61% | 100.00% | 96.35% | 92.05% | 98.39% |
| [capnp 0.23.2][capnp] | 2.33% | † | 42.86% | 72.68% | 81.40% | 10.14% |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 1.64% | 0.30% | 45.71% | 68.88% | 72.84% | 8.66% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 0.22% | 0.12% | 45.72% | 68.87% | 72.82% | 9.14% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 0.41% | 0.36% | 45.72% | 68.87% | 72.82% | 9.04% |
| [columnar 0.11.1][columnar] | 7.85% | 10.52% <span title="copy_from">*21.01%\**</span> | 100.00% | 96.35% | 92.05% | 97.33% |
| [databuf 0.5.0][databuf] | 6.13% | 2.78% | 100.00% | 96.35% | 92.05% | 95.22% |
| [dlhn 0.1.7][dlhn] | 2.48% | 2.19% | 100.00% | 96.35% | 92.05% | 95.42% |
| [flatbuffers 25.12.19][flatbuffers] | 31.34% | † | 100.00% | 96.35% | 92.05% | 94.02% |
| [flexbuffers 25.2.10][flexbuffers] | 0.14% | 0.16% | 22.55% | 43.54% | 39.42% | 5.49% |
| json:<br> [flexon 0.4.5][flexon] | 0.19% | 0.26% | 22.91% | 54.17% | 57.33% | 5.42% |
| json:<br> [serde_json 1.0.140][serde_json] | 0.16% | 0.15% | 22.91% | 54.17% | 57.33% | 5.42% |
| json:<br> [simd-json 0.15.1][simd-json] | 0.27% | 0.22% | 22.91% | 54.17% | 57.33% | 5.41% |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 4.67% | 3.00% | 80.00% | 85.54% | 81.83% | 81.00% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 0.80% | 0.91% | 73.85% | 79.79% | 77.01% | 11.31% |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 20.22% | 2.84% | 73.85% | 79.79% | 77.01% | 11.00% |
| [minicbor 1.0.0][minicbor] | 2.44% | 1.30% | 73.85% | 79.79% | 77.01% | 11.92% |
| [nachricht-serde 0.4.0][nachricht-serde] | 0.12% | 0.51% | 73.85% | 79.81% | 77.06% | 11.08% |
| [nanoserde 0.2.1][nanoserde] | 8.96% | 16.75% | 100.00% | 96.35% | 92.05% | 98.63% |
| [nibblecode 0.1.0][nibblecode] | 74.56% | † | 100.00% | 96.35% | 92.05% | 97.16% |
| [postcard 1.1.1][postcard] | 30.69% | 14.74% | 100.00% | 96.35% | 92.05% | 96.61% |
| [pot 3.0.1][pot] | 0.37% | 0.21% | 59.27% | 76.05% | 71.83% | 10.00% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*1.85%\**</span> <span title="populate + encode">*1.70%\**</span> | 1.36% | 68.57% | 77.75% | 76.64% | 11.62% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*0.95%\**</span> <span title="populate + encode">*0.47%\**</span> | 0.51% | 68.57% | 77.75% | 76.64% | 10.51% |
| [rkyv 0.8.10][rkyv] | 74.72% | <span title="unvalidated">*74.78%\**</span> <span title="validated upfront with error">*98.48%\**</span> | 100.00% | 96.35% | 92.05% | 100.00% |
| [ron 0.10.1][ron] | 0.08% | 0.03% | 27.04% | 57.77% | 60.48% | 5.68% |
| [savefile 0.18.6][savefile] | 100.00% | 75.27% | 100.00% | 96.35% | 92.05% | 96.64% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 2.89% | 3.59% | 100.00% | 96.35% | 92.05% | 97.65% |
| [serde-brief 0.1.1][serde-brief] | 0.84% | 0.41% | 38.10% | 64.58% | 72.23% | 8.94% |
| [serde_bare 0.5.0][serde_bare] | 2.29% | 3.19% | 100.00% | 96.35% | 92.05% | 96.78% |
| [speedy 0.8.7][speedy] | 74.23% | 98.90% | 100.00% | 96.35% | 92.05% | 98.64% |
| [wincode 0.2.4][wincode] | 74.58% | 100.00% | 100.00% | 96.35% | 92.05% | 97.26% |
| [wiring 0.2.4][wiring] | 74.43% | 43.76% | 100.00% | 96.34% | 92.05% | 97.00% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.12%\**</span> | <span title="validated on-demand with error">*1.97%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 5.71% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*50.02%\**</span> <span title="validated upfront with error">*2.79%\**</span> | <span title="unvalidated">*49.97%\**</span> <span title="validated upfront with error">*49.94%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*99.98%\**</span> <span title="validated upfront with error">*79.83%\**</span> | <span title="unvalidated">*99.99%\**</span> <span title="validated upfront with error">*99.99%\**</span> | <span title="unvalidated">*100.00%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*25.90%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*99.92%\**</span> | <span title="unvalidated">*79.52%\**</span> |

## `minecraft_savedata`

This data set is composed of Minecraft player saves that contain highly structured data.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Borrow | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*867.83 µs\**</span> <span title="prepend">*777.27 µs\**</span> | 3.0816 ms | 1.6948 ms | 489348 | 281173 | 249360 | 2.6392 ms |
| [bin-proto 0.12.3][bin-proto] | 1.9247 ms | 2.8233 ms | † | 566975 | 239350 | 231475 | 2.4522 ms |
| [bincode 2.0.1][bincode] | 309.74 µs | 1.7856 ms | 794.54 µs | 367413 | 221291 | 206242 | 2.2354 ms |
| [bincode 1.3.3][bincode1] | 590.83 µs | 2.3118 ms | 882.29 µs | 569975 | 240525 | 231884 | 2.4454 ms |
| [bitcode 0.6.6][bitcode] | 122.49 µs | 1.2609 ms | 179.61 µs | 327688 | 200947 | 182040 | 1.1082 ms |
| [borsh 1.5.7][borsh] | 557.28 µs | 1.8017 ms | † | 446595 | 234236 | 209834 | 2.0517 ms |
| [capnp 0.23.2][capnp] | 440.35 µs | † | † | 803896 | 335606 | 280744 | 3.5039 ms |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 747.35 µs | 4.6161 ms | 3.3619 ms | 1109831 | 344745 | 274333 | 3.4270 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 3.7910 ms | 10.505 ms | † | 1109821 | 344751 | 274345 | 3.4308 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 1.8370 ms | 4.8259 ms | 3.4499 ms | 1109821 | 344751 | 274345 | 3.4793 ms |
| [columnar 0.11.1][columnar] | 291.84 µs | 1.8945 ms <span title="copy_from">*775.54 µs\**</span> | † | 563728 | 249696 | 217582 | 1.5969 ms |
| [databuf 0.5.0][databuf] | 295.90 µs | 1.7519 ms | 822.20 µs | 356311 | 213062 | 198403 | 1.9177 ms |
| [dlhn 0.1.7][dlhn] | 684.47 µs | 2.6211 ms | † | 366496 | 220600 | 205586 | 1.9921 ms |
| [flatbuffers 25.12.19][flatbuffers] | 3.2532 ms | † | † | 849472 | 347816 | 294871 | 3.4231 ms |
| [flexbuffers 25.2.10][flexbuffers] | 7.8902 ms | 7.1942 ms | 5.9007 ms | 1187688 | 557642 | 553730 | 6.2888 ms |
| json:<br> [flexon 0.4.5][flexon] | 2.7829 ms | 4.5142 ms | † | 1623191 | 466527 | 359157 | 5.7061 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 3.9669 ms | 6.8928 ms | † | 1623191 | 466527 | 359157 | 5.9039 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 2.2308 ms | 4.5321 ms | † | 1623191 | 466527 | 359157 | 5.6513 ms |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 704.62 µs | 2.8241 ms | † | 391251 | 236877 | 220395 | 2.2103 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 1.4755 ms | 3.0177 ms | 1.6891 ms | 424533 | 245214 | 226077 | 2.2595 ms |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 380.73 µs | 2.1841 ms | 924.34 µs | 416025 | 243812 | 224965 | 2.2357 ms |
| [minicbor 1.0.0][minicbor] | 566.49 µs | 3.3382 ms | 1.8884 ms | 428773 | 249857 | 228630 | 2.2884 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 5.1135 ms | 3.9408 ms | 2.8131 ms | 449745 | 252432 | 230965 | 2.2907 ms |
| [nanoserde 0.2.1][nanoserde] | 268.52 µs | 1.8936 ms | † | 567975 | 239930 | 231872 | 2.4679 ms |
| [nibblecode 0.1.0][nibblecode] | 178.87 µs | † | † | 603928 | 430839 | 407675 | 3.6289 ms |
| [postcard 1.1.1][postcard] | 450.03 µs | 2.0944 ms | 825.05 µs | 367489 | 221913 | 207244 | 2.0073 ms |
| [pot 3.0.1][pot] | 2.4463 ms | 6.1111 ms | 5.0594 ms | 599125 | 299158 | 247675 | 2.6739 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*1.2742 ms\**</span> <span title="populate + encode">*3.0078 ms\**</span> | 3.4495 ms | † | 596811 | 305319 | 268737 | 2.9758 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*1.0740 ms\**</span> <span title="populate + encode">*3.0468 ms\**</span> | 3.8583 ms | † | 596811 | 305319 | 268737 | 2.9587 ms |
| [rkyv 0.8.10][rkyv] | 329.22 µs | <span title="unvalidated">*1.5013 ms\**</span> <span title="validated upfront with error">*1.8529 ms\**</span> | † | 603776 | 254776 | 219421 | 2.3730 ms |
| [ron 0.10.1][ron] | 8.0514 ms | 25.497 ms | 24.357 ms | 1465223 | 434935 | 342907 | 5.6967 ms |
| [savefile 0.18.6][savefile] | 213.27 µs | 1.8103 ms | † | 566991 | 239362 | 231478 | 2.4789 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 627.32 µs | 2.1064 ms | † | 356311 | 212976 | 198423 | 1.9802 ms |
| [serde-brief 0.1.1][serde-brief] | 1.1695 ms | 5.2209 ms | 3.5896 ms | 1276014 | 373898 | 293384 | 3.6176 ms |
| [serde_bare 0.5.0][serde_bare] | 755.63 µs | 2.3395 ms | † | 356311 | 213062 | 198403 | 1.9829 ms |
| [speedy 0.8.7][speedy] | 265.60 µs | 1.6715 ms | 544.80 µs | 449595 | 234970 | 210192 | 2.0609 ms |
| [wincode 0.2.4][wincode] | 195.24 µs | 1.6894 ms | 637.80 µs | 566975 | 239350 | 231475 | 2.4330 ms |
| [wiring 0.2.4][wiring] | 203.95 µs | 1.9176 ms | † | 566975 | 247810 | 225086 | 2.4482 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*89.559 ns\**</span> | <span title="validated on-demand with error">*423.16 ns\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 900.48 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.4907 ns\**</span> <span title="validated upfront with error">*2.1985 ms\**</span> | <span title="unvalidated">*1.4237 µs\**</span> <span title="validated upfront with error">*2.1994 ms\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.2449 ns\**</span> <span title="validated upfront with error">*254.34 µs\**</span> | <span title="unvalidated">*156.20 ns\**</span> <span title="validated upfront with error">*252.55 µs\**</span> | <span title="unvalidated">*724.25 ns\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.2498 ns\**</span> <span title="validated upfront with error">*337.38 µs\**</span> | <span title="unvalidated">*156.31 ns\**</span> <span title="validated upfront with error">*343.15 µs\**</span> | <span title="unvalidated">*731.18 ns\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Borrow | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*14.11%\**</span> <span title="prepend">*15.76%\**</span> | 25.17% | 10.60% | 66.96% | 71.47% | 73.00% | 41.99% |
| [bin-proto 0.12.3][bin-proto] | 6.36% | 27.47% | † | 57.80% | 83.96% | 78.64% | 45.19% |
| [bincode 2.0.1][bincode] | 39.55% | 43.43% | 22.61% | 89.19% | 90.81% | 88.27% | 49.58% |
| [bincode 1.3.3][bincode1] | 20.73% | 33.55% | 20.36% | 57.49% | 83.55% | 78.50% | 45.32% |
| [bitcode 0.6.6][bitcode] | 100.00% | 61.51% | 100.00% | 100.00% | 100.00% | 100.00% | 100.00% |
| [borsh 1.5.7][borsh] | 21.98% | 43.04% | † | 73.37% | 85.79% | 86.75% | 54.01% |
| [capnp 0.23.2][capnp] | 27.82% | † | † | 40.76% | 59.88% | 64.84% | 31.63% |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 16.39% | 16.80% | 5.34% | 29.53% | 58.29% | 66.36% | 32.34% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 3.23% | 7.38% | † | 29.53% | 58.29% | 66.35% | 32.30% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 6.67% | 16.07% | 5.21% | 29.53% | 58.29% | 66.35% | 31.85% |
| [columnar 0.11.1][columnar] | 41.97% | 40.94% <span title="copy_from">*100.00%\**</span> | † | 58.13% | 80.48% | 83.67% | 69.40% |
| [databuf 0.5.0][databuf] | 41.40% | 44.27% | 21.85% | 91.97% | 94.31% | 91.75% | 57.79% |
| [dlhn 0.1.7][dlhn] | 17.90% | 29.59% | † | 89.41% | 91.09% | 88.55% | 55.63% |
| [flatbuffers 25.12.19][flatbuffers] | 3.77% | † | † | 38.58% | 57.77% | 61.74% | 32.37% |
| [flexbuffers 25.2.10][flexbuffers] | 1.55% | 10.78% | 3.04% | 27.59% | 36.04% | 32.88% | 17.62% |
| json:<br> [flexon 0.4.5][flexon] | 4.40% | 17.18% | † | 20.19% | 43.07% | 50.69% | 19.42% |
| json:<br> [serde_json 1.0.140][serde_json] | 3.09% | 11.25% | † | 20.19% | 43.07% | 50.69% | 18.77% |
| json:<br> [simd-json 0.15.1][simd-json] | 5.49% | 17.11% | † | 20.19% | 43.07% | 50.69% | 19.61% |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 17.38% | 27.46% | † | 83.75% | 84.83% | 82.60% | 50.14% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 8.30% | 25.70% | 10.63% | 77.19% | 81.95% | 80.52% | 49.05% |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 32.17% | 35.51% | 19.43% | 78.77% | 82.42% | 80.92% | 49.57% |
| [minicbor 1.0.0][minicbor] | 21.62% | 23.23% | 9.51% | 76.42% | 80.42% | 79.62% | 48.43% |
| [nachricht-serde 0.4.0][nachricht-serde] | 2.40% | 19.68% | 6.38% | 72.86% | 79.60% | 78.82% | 48.38% |
| [nanoserde 0.2.1][nanoserde] | 45.62% | 40.96% | † | 57.69% | 83.75% | 78.51% | 44.90% |
| [nibblecode 0.1.0][nibblecode] | 68.48% | † | † | 54.26% | 46.64% | 44.65% | 30.54% |
| [postcard 1.1.1][postcard] | 27.22% | 37.03% | 21.77% | 89.17% | 90.55% | 87.84% | 55.21% |
| [pot 3.0.1][pot] | 5.01% | 12.69% | 3.55% | 54.69% | 67.17% | 73.50% | 41.45% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*9.61%\**</span> <span title="populate + encode">*4.07%\**</span> | 22.48% | † | 54.91% | 65.82% | 67.74% | 37.24% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*11.41%\**</span> <span title="populate + encode">*4.02%\**</span> | 20.10% | † | 54.91% | 65.82% | 67.74% | 37.46% |
| [rkyv 0.8.10][rkyv] | 37.21% | <span title="unvalidated">*51.66%\**</span> <span title="validated upfront with error">*41.86%\**</span> | † | 54.27% | 78.87% | 82.96% | 46.70% |
| [ron 0.10.1][ron] | 1.52% | 3.04% | 0.74% | 22.36% | 46.20% | 53.09% | 19.45% |
| [savefile 0.18.6][savefile] | 57.43% | 42.84% | † | 57.79% | 83.95% | 78.64% | 44.71% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 19.53% | 36.82% | † | 91.97% | 94.35% | 91.74% | 55.96% |
| [serde-brief 0.1.1][serde-brief] | 10.47% | 14.85% | 5.00% | 25.68% | 53.74% | 62.05% | 30.63% |
| [serde_bare 0.5.0][serde_bare] | 16.21% | 33.15% | † | 91.97% | 94.31% | 91.75% | 55.89% |
| [speedy 0.8.7][speedy] | 46.12% | 46.40% | 32.97% | 72.89% | 85.52% | 86.61% | 53.77% |
| [wincode 0.2.4][wincode] | 62.74% | 45.91% | 28.16% | 57.80% | 83.96% | 78.64% | 45.55% |
| [wiring 0.2.4][wiring] | 60.06% | 40.44% | † | 57.80% | 81.09% | 80.88% | 45.27% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.39%\**</span> | <span title="validated on-demand with error">*36.91%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 0.14% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*49.98%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*10.97%\**</span> <span title="validated upfront with error">*0.01%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.06%\**</span> | <span title="unvalidated">*100.00%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*99.61%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*99.93%\**</span> <span title="validated upfront with error">*0.05%\**</span> | <span title="unvalidated">*99.05%\**</span> |

## `mk48`

This data set is composed of mk48.io game updates that contain data with many exploitable patterns and invariants.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*4.5385 ms\**</span> <span title="prepend">*2.5126 ms\**</span> | 8.2728 ms | 1704643 | 1294259 | 1245668 | 11.677 ms |
| [bin-proto 0.12.3][bin-proto] | 5.1001 ms | 6.7538 ms | 1791489 | 1127998 | 1051146 | 10.172 ms |
| [bincode 2.0.1][bincode] | 1.2331 ms | 4.0228 ms | 1406257 | 1117802 | 1062438 | 9.3247 ms |
| [bincode 1.3.3][bincode1] | 3.8974 ms | 4.3583 ms | 1854234 | 1141994 | 1048745 | 10.305 ms |
| [bitcode 0.6.6][bitcode] | 703.38 µs | 2.3680 ms | 971318 | 878034 | 850340 | 2.8977 ms |
| [borsh 1.5.7][borsh] | 2.8646 ms | 2.8264 ms | 1521989 | 1108471 | 1038528 | 9.9148 ms |
| [capnp 0.23.2][capnp] | 2.1392 ms | † | 2724288 | 1546992 | 1239111 | 14.486 ms |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 3.2323 ms | 18.244 ms | 6012539 | 1695215 | 1464951 | 21.153 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 23.728 ms | 55.204 ms | 6012373 | 1695146 | 1465025 | 21.134 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 9.6191 ms | 20.464 ms | 6012373 | 1695146 | 1465025 | 21.339 ms |
| [columnar 0.11.1][columnar] | 907.31 µs | 3.7704 ms <span title="copy_from">*1.2476 ms\**</span> | 1544752 | 996728 | 897073 | 4.7561 ms |
| [databuf 0.5.0][databuf] | 1.3283 ms | 3.8440 ms | 1319999 | 1062631 | 1008334 | 8.9072 ms |
| [dlhn 0.1.7][dlhn] | 4.4983 ms | 7.5018 ms | 1311281 | 1077520 | 1046095 | 8.5577 ms |
| [flatbuffers 25.12.19][flatbuffers] | 4.9330 ms | † | 2325620 | 1439185 | 1268060 | 13.766 ms |
| [flexbuffers 25.2.10][flexbuffers] | 40.067 ms | 36.796 ms | 5352680 | 2658295 | 2777967 | 35.377 ms |
| json:<br> [flexon 0.4.5][flexon] | 15.295 ms | 23.590 ms | 9390461 | 2391679 | 1842767 | 34.782 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 21.966 ms | 31.679 ms | 9390461 | 2391679 | 1842767 | 34.920 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 12.046 ms | 25.435 ms | 9390461 | 2391679 | 1842767 | 34.633 ms |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 1.6776 ms | 6.1066 ms | 1458773 | 1156055 | 1137788 | 9.6392 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 10.812 ms | 10.837 ms | 1745322 | 1261627 | 1228923 | 11.405 ms |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 1.8336 ms | 5.8747 ms | 1794467 | 1273669 | 1242301 | 11.825 ms |
| [minicbor 1.0.0][minicbor] | 2.4286 ms | 11.365 ms | 1777386 | 1276218 | 1252558 | 12.754 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 30.449 ms | 16.789 ms | 1770060 | 1277755 | 1263362 | 12.418 ms |
| [nanoserde 0.2.1][nanoserde] | 1.2539 ms | 2.7864 ms | 1812404 | 1134820 | 1053109 | 10.350 ms |
| [nibblecode 0.1.0][nibblecode] | 505.37 µs | † | 2075936 | 1503435 | 1396519 | 13.931 ms |
| [postcard 1.1.1][postcard] | 1.8757 ms | 4.1718 ms | 1311281 | 1083900 | 1041434 | 8.7904 ms |
| [pot 3.0.1][pot] | 14.868 ms | 29.459 ms | 2604812 | 1482233 | 1298928 | 16.233 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*5.4435 ms\**</span> <span title="populate + encode">*9.2916 ms\**</span> | 8.6185 ms | 1859886 | 1338076 | 1295351 | 12.412 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*5.6350 ms\**</span> <span title="populate + encode">*12.860 ms\**</span> | 11.899 ms | 1859886 | 1338076 | 1295351 | 12.166 ms |
| [rkyv 0.8.10][rkyv] | 985.43 µs | <span title="unvalidated">*2.2009 ms\**</span> <span title="validated upfront with error">*2.6485 ms\**</span> | 2075936 | 1383779 | 1210377 | 13.014 ms |
| [ron 0.10.1][ron] | 42.160 ms | 156.18 ms | 8677703 | 2233642 | 1826180 | 34.297 ms |
| [savefile 0.18.6][savefile] | 876.53 µs | 2.5682 ms | 1791505 | 1128012 | 1051153 | 10.186 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 3.1780 ms | 3.3336 ms | 1319999 | 1064380 | 1010708 | 9.0863 ms |
| [serde-brief 0.1.1][serde-brief] | 5.4366 ms | 21.508 ms | 6951772 | 1796265 | 1567819 | 24.690 ms |
| [serde_bare 0.5.0][serde_bare] | 4.9209 ms | 5.0159 ms | 1319999 | 1062645 | 1008349 | 9.0217 ms |
| [speedy 0.8.7][speedy] | 769.40 µs | 2.4591 ms | 1584734 | 1119837 | 1037992 | 10.251 ms |
| [wincode 0.2.4][wincode] | 578.74 µs | 2.3881 ms | 1791489 | 1127998 | 1051146 | 10.152 ms |
| [wiring 0.2.4][wiring] | 651.89 µs | 2.7832 ms | 1791489 | 1156963 | 1082815 | 10.446 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*82.079 ns\**</span> | <span title="validated on-demand with error">*726.49 ns\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 57.953 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.4898 ns\**</span> <span title="validated upfront with error">*5.6219 ms\**</span> | <span title="unvalidated">*2.7462 µs\**</span> <span title="validated upfront with error">*5.6253 ms\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.2449 ns\**</span> <span title="validated upfront with error">*345.01 µs\**</span> | <span title="unvalidated">*378.72 ns\**</span> <span title="validated upfront with error">*345.84 µs\**</span> | <span title="unvalidated">*238.34 ns\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.2456 ns\**</span> <span title="validated upfront with error">*442.31 µs\**</span> | <span title="unvalidated">*385.75 ns\**</span> <span title="validated upfront with error">*448.15 µs\**</span> | <span title="unvalidated">*235.42 ns\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*11.14%\**</span> <span title="prepend">*20.11%\**</span> | 15.08% | 56.98% | 67.84% | 68.26% | 24.82% |
| [bin-proto 0.12.3][bin-proto] | 9.91% | 18.47% | 54.22% | 77.84% | 80.90% | 28.49% |
| [bincode 2.0.1][bincode] | 40.98% | 31.01% | 69.07% | 78.55% | 80.04% | 31.08% |
| [bincode 1.3.3][bincode1] | 12.97% | 28.63% | 52.38% | 76.89% | 81.08% | 28.12% |
| [bitcode 0.6.6][bitcode] | 71.85% | 52.69% | 100.00% | 100.00% | 100.00% | 100.00% |
| [borsh 1.5.7][borsh] | 17.64% | 44.14% | 63.82% | 79.21% | 81.88% | 29.23% |
| [capnp 0.23.2][capnp] | 23.62% | † | 35.65% | 56.76% | 68.63% | 20.00% |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 15.63% | 6.84% | 16.15% | 51.79% | 58.05% | 13.70% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 2.13% | 2.26% | 16.16% | 51.80% | 58.04% | 13.71% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 5.25% | 6.10% | 16.16% | 51.80% | 58.04% | 13.58% |
| [columnar 0.11.1][columnar] | 55.70% | 33.09% <span title="copy_from">*100.00%\**</span> | 62.88% | 88.09% | 94.79% | 60.93% |
| [databuf 0.5.0][databuf] | 38.05% | 32.46% | 73.58% | 82.63% | 84.33% | 32.53% |
| [dlhn 0.1.7][dlhn] | 11.23% | 16.63% | 74.07% | 81.49% | 81.29% | 33.86% |
| [flatbuffers 25.12.19][flatbuffers] | 10.24% | † | 41.77% | 61.01% | 67.06% | 21.05% |
| [flexbuffers 25.2.10][flexbuffers] | 1.26% | 3.39% | 18.15% | 33.03% | 30.61% | 8.19% |
| json:<br> [flexon 0.4.5][flexon] | 3.30% | 5.29% | 10.34% | 36.71% | 46.14% | 8.33% |
| json:<br> [serde_json 1.0.140][serde_json] | 2.30% | 3.94% | 10.34% | 36.71% | 46.14% | 8.30% |
| json:<br> [simd-json 0.15.1][simd-json] | 4.20% | 4.91% | 10.34% | 36.71% | 46.14% | 8.37% |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 30.12% | 20.43% | 66.58% | 75.95% | 74.74% | 30.06% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 4.67% | 11.51% | 55.65% | 69.60% | 69.19% | 25.41% |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 27.56% | 21.24% | 54.13% | 68.94% | 68.45% | 24.50% |
| [minicbor 1.0.0][minicbor] | 20.81% | 10.98% | 54.65% | 68.80% | 67.89% | 22.72% |
| [nachricht-serde 0.4.0][nachricht-serde] | 1.66% | 7.43% | 54.87% | 68.72% | 67.31% | 23.33% |
| [nanoserde 0.2.1][nanoserde] | 40.30% | 44.77% | 53.59% | 77.37% | 80.75% | 28.00% |
| [nibblecode 0.1.0][nibblecode] | 100.00% | † | 46.79% | 58.40% | 60.89% | 20.80% |
| [postcard 1.1.1][postcard] | 26.94% | 29.91% | 74.07% | 81.01% | 81.65% | 32.96% |
| [pot 3.0.1][pot] | 3.40% | 4.24% | 37.29% | 59.24% | 65.46% | 17.85% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*9.28%\**</span> <span title="populate + encode">*5.44%\**</span> | 14.48% | 52.22% | 65.62% | 65.65% | 23.35% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*8.97%\**</span> <span title="populate + encode">*3.93%\**</span> | 10.48% | 52.22% | 65.62% | 65.65% | 23.82% |
| [rkyv 0.8.10][rkyv] | 51.28% | <span title="unvalidated">*56.69%\**</span> <span title="validated upfront with error">*47.11%\**</span> | 46.79% | 63.45% | 70.25% | 22.27% |
| [ron 0.10.1][ron] | 1.20% | 0.80% | 11.19% | 39.31% | 46.56% | 8.45% |
| [savefile 0.18.6][savefile] | 57.66% | 48.58% | 54.22% | 77.84% | 80.90% | 28.45% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 15.90% | 37.43% | 73.58% | 82.49% | 84.13% | 31.89% |
| [serde-brief 0.1.1][serde-brief] | 9.30% | 5.80% | 13.97% | 48.88% | 54.24% | 11.74% |
| [serde_bare 0.5.0][serde_bare] | 10.27% | 24.87% | 73.58% | 82.63% | 84.33% | 32.12% |
| [speedy 0.8.7][speedy] | 65.68% | 50.73% | 61.29% | 78.41% | 81.92% | 28.27% |
| [wincode 0.2.4][wincode] | 87.32% | 52.24% | 54.22% | 77.84% | 80.90% | 28.54% |
| [wiring 0.2.4][wiring] | 77.52% | 44.83% | 54.22% | 75.89% | 78.53% | 27.74% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.52%\**</span> | <span title="validated on-demand with error">*52.13%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 2.15% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*50.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*13.79%\**</span> <span title="validated upfront with error">*0.01%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.11%\**</span> | <span title="unvalidated">*98.77%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*99.94%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*98.18%\**</span> <span title="validated upfront with error">*0.08%\**</span> | <span title="unvalidated">*100.00%\**</span> |

[bilrost]: https://crates.io/crates/bilrost/0.1013.0
[bin-proto]: https://crates.io/crates/bin-proto/0.12.3
[bincode]: https://crates.io/crates/bincode/2.0.1
[bincode1]: https://crates.io/crates/bincode/1.3.3
[bitcode]: https://crates.io/crates/bitcode/0.6.6
[borsh]: https://crates.io/crates/borsh/1.5.7
[capnp]: https://crates.io/crates/capnp/0.23.2
[cbor4ii]: https://crates.io/crates/cbor4ii/1.0.0
[ciborium]: https://crates.io/crates/ciborium/0.2.2
[columnar]: https://crates.io/crates/columnar/0.11.1
[databuf]: https://crates.io/crates/databuf/0.5.0
[dlhn]: https://crates.io/crates/dlhn/0.1.7
[flatbuffers]: https://crates.io/crates/flatbuffers/25.12.19
[flexbuffers]: https://crates.io/crates/flexbuffers/25.2.10
[flexon]: https://crates.io/crates/flexon/0.4.5
[minicbor]: https://crates.io/crates/minicbor/1.0.0
[msgpacker]: https://crates.io/crates/msgpacker/0.4.8
[nachricht-serde]: https://crates.io/crates/nachricht-serde/0.4.0
[nanoserde]: https://crates.io/crates/nanoserde/0.2.1
[nibblecode]: https://crates.io/crates/nibblecode/0.1.0
[parity-scale-codec]: https://crates.io/crates/parity-scale-codec/3.7.5
[postcard]: https://crates.io/crates/postcard/1.1.1
[pot]: https://crates.io/crates/pot/3.0.1
[prost]: https://crates.io/crates/prost/0.14.1
[protobuf]: https://crates.io/crates/protobuf/3.7.2
[rkyv]: https://crates.io/crates/rkyv/0.8.10
[rmp-serde]: https://crates.io/crates/rmp-serde/1.3.0
[ron]: https://crates.io/crates/ron/0.10.1
[savefile]: https://crates.io/crates/savefile/0.18.6
[serde-brief]: https://crates.io/crates/serde-brief/0.1.1
[serde_bare]: https://crates.io/crates/serde_bare/0.5.0
[serde_cbor]: https://crates.io/crates/serde_cbor/0.11.2
[serde_json]: https://crates.io/crates/serde_json/1.0.140
[simd-json]: https://crates.io/crates/simd-json/0.15.1
[speedy]: https://crates.io/crates/speedy/0.8.7
[wincode]: https://crates.io/crates/wincode/0.2.4
[wiring]: https://crates.io/crates/wiring/0.2.4
[zerompk]: https://crates.io/crates/zerompk/0.3.2


## Footnotes:

\* *mouse over for situational details*

† *this deserialization capability is not supported*

‡ *buffer mutation is not supported (`capnp` and `flatbuffers` may but not for rust)*
