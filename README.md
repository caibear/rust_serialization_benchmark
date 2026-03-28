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

## Last updated: 2026-03-28 00:08:13

<details><summary>Runtime info</summary>

### `rustc` version

```
rustc 1.96.0-nightly (23903d01c 2026-03-26)
binary: rustc
commit-hash: 23903d01c237d7c7d4fb62b82ca846bc45de4e0c
commit-date: 2026-03-26
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
BogoMIPS:                                4890.87
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
| [bilrost 0.1013.0][bilrost] | <span title="encode">*471.18 µs\**</span> <span title="prepend">*425.58 µs\**</span> | 2.5633 ms | 915.73 µs | 804955 | 328941 | 284849 | 4.3522 ms |
| [bin-proto 0.12.3][bin-proto] | 4.5352 ms | 4.7841 ms | † | 1045784 | 373127 | 311553 | 4.5352 ms |
| [bincode 2.0.1][bincode] | 352.06 µs | 2.1580 ms | 685.21 µs | 741295 | 303944 | 256422 | 3.6488 ms |
| [bincode 1.3.3][bincode1] | 549.57 µs | 2.0184 ms | 609.75 µs | 1045784 | 373127 | 311553 | 4.6270 ms |
| [bitcode 0.6.6][bitcode] | 141.04 µs | 1.4651 ms | 60.154 µs | 703710 | 288826 | 227322 | 2.5512 ms |
| [borsh 1.5.7][borsh] | 561.46 µs | 2.1286 ms | † | 885780 | 362204 | 286248 | 4.2162 ms |
| [capnp 0.23.2][capnp] | 462.16 µs | † | † | 1443216 | 513986 | 426532 | 6.5071 ms |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 611.99 µs | 5.3127 ms | 3.4207 ms | 1407835 | 403440 | 323561 | 5.0397 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 4.0809 ms | 11.065 ms | † | 1407835 | 403440 | 323561 | 5.0765 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 1.9156 ms | 4.9130 ms | 3.2942 ms | 1407835 | 403440 | 323561 | 5.3363 ms |
| [columnar 0.11.1][columnar] | 257.09 µs | 2.1666 ms <span title="copy_from">*819.19 µs\**</span> | † | 1045928 | 370212 | 293907 | 4.2328 ms |
| [databuf 0.5.0][databuf] | 261.75 µs | 2.0281 ms | 682.51 µs | 765778 | 311715 | 263914 | 3.6121 ms |
| [dlhn 0.1.7][dlhn] | 680.01 µs | 2.5890 ms | † | 724953 | 301446 | 253056 | 3.3739 ms |
| [flatbuffers 25.12.19][flatbuffers] | 1.0408 ms | † | † | 1276368 | 468539 | 388381 | 4.8538 ms |
| [flexbuffers 25.2.10][flexbuffers] | 6.6413 ms | 7.5498 ms | 5.9139 ms | 1829756 | 714318 | 691541 | 8.8123 ms |
| json:<br> [flexon 0.4.5][flexon] | 2.7870 ms | 3.9485 ms | † | 1827461 | 470560 | 360727 | 5.5592 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 3.8134 ms | 6.0812 ms | † | 1827461 | 470560 | 360727 | 5.9978 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 2.1290 ms | 4.8254 ms | † | 1827461 | 470560 | 360727 | 5.6363 ms |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 1.1051 ms | 2.5995 ms | † | 764996 | 315291 | 264212 | 3.7692 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 1.3591 ms | 3.1645 ms | 1.4194 ms | 784997 | 325384 | 277608 | 3.9174 ms |
| [minicbor 1.0.0][minicbor] | 516.63 µs | 3.1454 ms | 1.4602 ms | 817830 | 332671 | 284034 | 3.9922 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 5.3391 ms | 4.1828 ms | 2.6040 ms | 818669 | 332556 | 284797 | 4.2463 ms |
| [nanoserde 0.2.1][nanoserde] | 262.26 µs | 2.1067 ms | † | 1045784 | 373127 | 311553 | 4.3006 ms |
| [nibblecode 0.1.0][nibblecode] | 199.04 µs | † | † | 1011487 | 473998 | 404667 | 5.5449 ms |
| [postcard 1.1.1][postcard] | 421.95 µs | 2.3031 ms | 728.14 µs | 724953 | 302399 | 252968 | 3.3187 ms |
| [pot 3.0.1][pot] | 2.2714 ms | 6.6162 ms | 4.9600 ms | 971922 | 372513 | 303636 | 4.4315 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*939.38 µs\**</span> <span title="populate + encode">*2.5090 ms\**</span> | 3.3619 ms | † | 884628 | 363130 | 314959 | 4.4152 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*1.2064 ms\**</span> <span title="populate + encode">*3.0725 ms\**</span> | 3.9250 ms | † | 884628 | 363130 | 314959 | 4.3638 ms |
| [rkyv 0.8.10][rkyv] | 250.27 µs | <span title="unvalidated">*1.5663 ms\**</span> <span title="validated upfront with error">*1.9149 ms\**</span> | † | 1011488 | 393526 | 325965 | 4.6819 ms |
| [ron 0.10.1][ron] | 12.457 ms | 23.177 ms | 21.628 ms | 1607459 | 449158 | 349324 | 5.6190 ms |
| [savefile 0.18.6][savefile] | 197.38 µs | 2.0923 ms | † | 1045800 | 373139 | 311562 | 4.1731 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 662.37 µs | 2.3717 ms | † | 765778 | 311743 | 263822 | 3.6017 ms |
| [serde-brief 0.1.1][serde-brief] | 1.3636 ms | 4.7466 ms | 3.0506 ms | 1584946 | 413733 | 339964 | 4.9646 ms |
| [serde_bare 0.5.0][serde_bare] | 687.46 µs | 2.0895 ms | † | 765778 | 311715 | 263914 | 3.5471 ms |
| [speedy 0.8.7][speedy] | 204.53 µs | 1.7473 ms | 364.14 µs | 885780 | 362204 | 286248 | 3.9948 ms |
| [wincode 0.2.4][wincode] | 172.52 µs | 1.9264 ms | 486.03 µs | 1045784 | 373127 | 311553 | 4.2350 ms |
| [wiring 0.2.4][wiring] | 193.61 µs | 2.1004 ms | † | 1045784 | 337930 | 275808 | 3.6765 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*83.883 ns\**</span> | <span title="validated on-demand with error">*135.97 µs\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 23.497 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.4908 ns\**</span> <span title="validated upfront with error">*2.1111 ms\**</span> | <span title="unvalidated">*49.724 µs\**</span> <span title="validated upfront with error">*2.1873 ms\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.2450 ns\**</span> <span title="validated upfront with error">*237.13 µs\**</span> | <span title="unvalidated">*10.530 µs\**</span> <span title="validated upfront with error">*249.27 µs\**</span> | <span title="unvalidated">*7.5356 µs\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.2449 ns\**</span> <span title="validated upfront with error">*339.44 µs\**</span> | <span title="unvalidated">*10.639 µs\**</span> <span title="validated upfront with error">*351.29 µs\**</span> | <span title="unvalidated">*7.4074 µs\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Borrow | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*29.93%\**</span> <span title="prepend">*33.14%\**</span> | 31.96% | 6.57% | 87.42% | 87.80% | 79.80% | 58.62% |
| [bin-proto 0.12.3][bin-proto] | 3.11% | 17.12% | † | 67.29% | 77.41% | 72.96% | 56.25% |
| [bincode 2.0.1][bincode] | 40.06% | 37.96% | 8.78% | 94.93% | 95.03% | 88.65% | 69.92% |
| [bincode 1.3.3][bincode1] | 25.66% | 40.59% | 9.87% | 67.29% | 77.41% | 72.96% | 55.14% |
| [bitcode 0.6.6][bitcode] | 100.00% | 55.91% | 100.00% | 100.00% | 100.00% | 100.00% | 100.00% |
| [borsh 1.5.7][borsh] | 25.12% | 38.48% | † | 79.45% | 79.74% | 79.41% | 60.51% |
| [capnp 0.23.2][capnp] | 30.52% | † | † | 48.76% | 56.19% | 53.30% | 39.21% |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 23.05% | 15.42% | 1.76% | 49.99% | 71.59% | 70.26% | 50.62% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 3.46% | 7.40% | † | 49.99% | 71.59% | 70.26% | 50.26% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 7.36% | 16.67% | 1.83% | 49.99% | 71.59% | 70.26% | 47.81% |
| [columnar 0.11.1][columnar] | 54.86% | 37.81% <span title="copy_from">*100.00%\**</span> | † | 67.28% | 78.02% | 77.34% | 60.27% |
| [databuf 0.5.0][databuf] | 53.88% | 40.39% | 8.81% | 91.89% | 92.66% | 86.13% | 70.63% |
| [dlhn 0.1.7][dlhn] | 20.74% | 31.64% | † | 97.07% | 95.81% | 89.83% | 75.62% |
| [flatbuffers 25.12.19][flatbuffers] | 13.55% | † | † | 55.13% | 61.64% | 58.53% | 52.56% |
| [flexbuffers 25.2.10][flexbuffers] | 2.12% | 10.85% | 1.02% | 38.46% | 40.43% | 32.87% | 28.95% |
| json:<br> [flexon 0.4.5][flexon] | 5.06% | 20.75% | † | 38.51% | 61.38% | 63.02% | 45.89% |
| json:<br> [serde_json 1.0.140][serde_json] | 3.70% | 13.47% | † | 38.51% | 61.38% | 63.02% | 42.54% |
| json:<br> [simd-json 0.15.1][simd-json] | 6.62% | 16.98% | † | 38.51% | 61.38% | 63.02% | 45.26% |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 12.76% | 31.51% | † | 91.99% | 91.61% | 86.04% | 67.69% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 10.38% | 25.89% | 4.24% | 89.64% | 88.76% | 81.89% | 65.12% |
| [minicbor 1.0.0][minicbor] | 27.30% | 26.04% | 4.12% | 86.05% | 86.82% | 80.03% | 63.90% |
| [nachricht-serde 0.4.0][nachricht-serde] | 2.64% | 19.58% | 2.31% | 85.96% | 86.85% | 79.82% | 60.08% |
| [nanoserde 0.2.1][nanoserde] | 53.78% | 38.88% | † | 67.29% | 77.41% | 72.96% | 59.32% |
| [nibblecode 0.1.0][nibblecode] | 70.86% | † | † | 69.57% | 60.93% | 56.18% | 46.01% |
| [postcard 1.1.1][postcard] | 33.43% | 35.57% | 8.26% | 97.07% | 95.51% | 89.86% | 76.87% |
| [pot 3.0.1][pot] | 6.21% | 12.38% | 1.21% | 72.40% | 77.53% | 74.87% | 57.57% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*15.01%\**</span> <span title="populate + encode">*5.62%\**</span> | 24.37% | † | 79.55% | 79.54% | 72.18% | 57.78% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*11.69%\**</span> <span title="populate + encode">*4.59%\**</span> | 20.87% | † | 79.55% | 79.54% | 72.18% | 58.46% |
| [rkyv 0.8.10][rkyv] | 56.36% | <span title="unvalidated">*52.30%\**</span> <span title="validated upfront with error">*42.78%\**</span> | † | 69.57% | 73.39% | 69.74% | 54.49% |
| [ron 0.10.1][ron] | 1.13% | 3.53% | 0.28% | 43.78% | 64.30% | 65.07% | 45.40% |
| [savefile 0.18.6][savefile] | 71.46% | 39.15% | † | 67.29% | 77.40% | 72.96% | 61.13% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 21.29% | 34.54% | † | 91.89% | 92.65% | 86.16% | 70.83% |
| [serde-brief 0.1.1][serde-brief] | 10.34% | 17.26% | 1.97% | 44.40% | 69.81% | 66.87% | 51.39% |
| [serde_bare 0.5.0][serde_bare] | 20.52% | 39.21% | † | 91.89% | 92.66% | 86.13% | 71.92% |
| [speedy 0.8.7][speedy] | 68.96% | 46.88% | 16.52% | 79.45% | 79.74% | 79.41% | 63.86% |
| [wincode 0.2.4][wincode] | 81.75% | 42.52% | 12.38% | 67.29% | 77.41% | 72.96% | 60.24% |
| [wiring 0.2.4][wiring] | 72.85% | 39.00% | † | 67.29% | 85.47% | 82.42% | 69.39% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.48%\**</span> | <span title="validated on-demand with error">*7.74%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 5.30% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*49.98%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*21.18%\**</span> <span title="validated upfront with error">*0.48%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*99.99%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*4.22%\**</span> | <span title="unvalidated">*98.30%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*98.98%\**</span> <span title="validated upfront with error">*3.00%\**</span> | <span title="unvalidated">*100.00%\**</span> |

## `mesh`

This data set is a single mesh. The mesh contains an array of triangles, each of which has three vertices and a normal vector.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*7.3803 ms\**</span> <span title="prepend">*8.7573 ms\**</span> | 7.7683 ms | 8625005 | 6443961 | 6231572 | 74.918 ms |
| [bin-proto 0.12.3][bin-proto] | 8.8773 ms | 10.540 ms | 6000008 | 5378500 | 5346908 | 8.7959 ms |
| [bincode 2.0.1][bincode] | 2.8914 ms | 1.0796 ms | 6000005 | 5378497 | 5346882 | 9.0606 ms |
| [bincode 1.3.3][bincode1] | 5.8501 ms | 4.8197 ms | 6000008 | 5378500 | 5346908 | 8.9160 ms |
| [bitcode 0.6.6][bitcode] | 1.5081 ms | 823.98 µs | 6000006 | 5182295 | 4921841 | 14.668 ms |
| [borsh 1.5.7][borsh] | 6.1450 ms | 4.4504 ms | 6000004 | 5378496 | 5346866 | 9.0469 ms |
| [capnp 0.23.2][capnp] | 6.4398 ms | † | 14000088 | 7130367 | 6046182 | 83.017 ms |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 9.0000 ms | 49.957 ms | 13125016 | 7524114 | 6757437 | 95.536 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 65.972 ms | 114.09 ms | 13122324 | 7524660 | 6759128 | 93.570 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 34.460 ms | 41.913 ms | 13122324 | 7524660 | 6759128 | 94.183 ms |
| [columnar 0.11.1][columnar] | 2.0197 ms | 1.4512 ms <span title="copy_from">*689.73 µs\**</span> | 6000120 | 5378435 | 5347039 | 8.9292 ms |
| [databuf 0.5.0][databuf] | 2.4183 ms | 5.4153 ms | 6000003 | 5378495 | 5346897 | 8.9116 ms |
| [dlhn 0.1.7][dlhn] | 5.2121 ms | 7.0992 ms | 6000003 | 5378495 | 5346897 | 8.8883 ms |
| [flatbuffers 25.12.19][flatbuffers] | 450.55 µs | † | 6000024 | 5378434 | 5346878 | 8.7716 ms |
| [flexbuffers 25.2.10][flexbuffers] | 103.57 ms | 92.525 ms | 26609424 | 11901040 | 12486322 | 158.78 ms |
| json:<br> [flexon 0.4.5][flexon] | 76.681 ms | 55.568 ms | 26192883 | 9566084 | 8584671 | 164.00 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 88.183 ms | 100.25 ms | 26192883 | 9566084 | 8584671 | 159.66 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 54.150 ms | 68.174 ms | 26192883 | 9566084 | 8584671 | 161.23 ms |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 2.0968 ms | 5.3510 ms | 7500005 | 6058442 | 6014500 | 11.010 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 18.572 ms | 16.531 ms | 8125006 | 6494876 | 6391037 | 71.561 ms |
| [minicbor 1.0.0][minicbor] | 5.2015 ms | 11.837 ms | 8125006 | 6494907 | 6390894 | 70.855 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 121.18 ms | 28.058 ms | 8125037 | 6493484 | 6386940 | 73.421 ms |
| [nanoserde 0.2.1][nanoserde] | 1.7008 ms | 835.55 µs | 6000008 | 5378500 | 5346908 | 8.9733 ms |
| [nibblecode 0.1.0][nibblecode] | 149.98 µs | † | 6000008 | 5378500 | 5346908 | 8.8048 ms |
| [postcard 1.1.1][postcard] | 483.79 µs | 1.2712 ms | 6000003 | 5378495 | 5346897 | 8.9013 ms |
| [pot 3.0.1][pot] | 39.005 ms | 70.155 ms | 10122342 | 6814618 | 6852252 | 85.188 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*7.8465 ms\**</span> <span title="populate + encode">*8.6248 ms\**</span> | 13.916 ms | 8750000 | 6665735 | 6421877 | 73.994 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*14.396 ms\**</span> <span title="populate + encode">*31.066 ms\**</span> | 29.509 ms | 8750000 | 6665735 | 6421877 | 81.357 ms |
| [rkyv 0.8.10][rkyv] | 149.89 µs | <span title="unvalidated">*153.70 µs\**</span> <span title="validated upfront with error">*152.34 µs\**</span> | 6000008 | 5378500 | 5346872 | 9.0166 ms |
| [ron 0.10.1][ron] | 171.06 ms | 516.46 ms | 22192885 | 8970395 | 8137334 | 161.93 ms |
| [savefile 0.18.6][savefile] | 150.26 µs | 150.30 µs | 6000024 | 5378519 | 5346896 | 8.8584 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 4.8277 ms | 4.1126 ms | 6000004 | 5378496 | 5346866 | 9.1508 ms |
| [serde-brief 0.1.1][serde-brief] | 17.314 ms | 37.353 ms | 15750015 | 8024540 | 6813667 | 97.516 ms |
| [serde_bare 0.5.0][serde_bare] | 6.0431 ms | 4.9336 ms | 6000003 | 5378495 | 5346897 | 8.9690 ms |
| [speedy 0.8.7][speedy] | 150.39 µs | 151.04 µs | 6000004 | 5378496 | 5346866 | 8.8065 ms |
| [wincode 0.2.4][wincode] | 151.79 µs | 151.06 µs | 6000008 | 5378500 | 5346908 | 8.8547 ms |
| [wiring 0.2.4][wiring] | 151.11 µs | 345.42 µs | 6000008 | 5378952 | 5346905 | 8.7946 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*111.68 ns\**</span> | <span title="validated on-demand with error">*2.0432 ms\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 21.902 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.4926 ns\**</span> <span title="validated upfront with error">*44.182 ns\**</span> | <span title="unvalidated">*78.154 µs\**</span> <span title="validated upfront with error">*78.165 µs\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.2443 ns\**</span> <span title="validated upfront with error">*1.5569 ns\**</span> | <span title="unvalidated">*38.912 µs\**</span> <span title="validated upfront with error">*38.911 µs\**</span> | <span title="unvalidated">*79.719 µs\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.2449 ns\**</span> <span title="validated upfront with error">*5.3030 ns\**</span> | <span title="unvalidated">*38.903 µs\**</span> <span title="validated upfront with error">*39.074 µs\**</span> | <span title="unvalidated">*76.338 µs\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*2.03%\**</span> <span title="prepend">*1.71%\**</span> | 1.93% | 69.57% | 80.42% | 78.98% | 11.71% |
| [bin-proto 0.12.3][bin-proto] | 1.69% | 1.43% | 100.00% | 96.35% | 92.05% | 99.72% |
| [bincode 2.0.1][bincode] | 5.18% | 13.92% | 100.00% | 96.35% | 92.05% | 96.81% |
| [bincode 1.3.3][bincode1] | 2.56% | 3.12% | 100.00% | 96.35% | 92.05% | 98.38% |
| [bitcode 0.6.6][bitcode] | 9.94% | 18.24% | 100.00% | 100.00% | 100.00% | 59.80% |
| [borsh 1.5.7][borsh] | 2.44% | 3.38% | 100.00% | 96.35% | 92.05% | 96.96% |
| [capnp 0.23.2][capnp] | 2.33% | † | 42.86% | 72.68% | 81.40% | 10.57% |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 1.67% | 0.30% | 45.71% | 68.88% | 72.84% | 9.18% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 0.23% | 0.13% | 45.72% | 68.87% | 72.82% | 9.37% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 0.43% | 0.36% | 45.72% | 68.87% | 72.82% | 9.31% |
| [columnar 0.11.1][columnar] | 7.42% | 10.36% <span title="copy_from">*21.79%\**</span> | 100.00% | 96.35% | 92.05% | 98.24% |
| [databuf 0.5.0][databuf] | 6.20% | 2.78% | 100.00% | 96.35% | 92.05% | 98.43% |
| [dlhn 0.1.7][dlhn] | 2.88% | 2.12% | 100.00% | 96.35% | 92.05% | 98.69% |
| [flatbuffers 25.12.19][flatbuffers] | 33.27% | † | 100.00% | 96.35% | 92.05% | 100.00% |
| [flexbuffers 25.2.10][flexbuffers] | 0.14% | 0.16% | 22.55% | 43.54% | 39.42% | 5.52% |
| json:<br> [flexon 0.4.5][flexon] | 0.20% | 0.27% | 22.91% | 54.17% | 57.33% | 5.35% |
| json:<br> [serde_json 1.0.140][serde_json] | 0.17% | 0.15% | 22.91% | 54.17% | 57.33% | 5.49% |
| json:<br> [simd-json 0.15.1][simd-json] | 0.28% | 0.22% | 22.91% | 54.17% | 57.33% | 5.44% |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 7.15% | 2.81% | 80.00% | 85.54% | 81.83% | 79.67% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 0.81% | 0.91% | 73.85% | 79.79% | 77.01% | 12.26% |
| [minicbor 1.0.0][minicbor] | 2.88% | 1.27% | 73.85% | 79.79% | 77.01% | 12.38% |
| [nachricht-serde 0.4.0][nachricht-serde] | 0.12% | 0.54% | 73.85% | 79.81% | 77.06% | 11.95% |
| [nanoserde 0.2.1][nanoserde] | 8.81% | 17.99% | 100.00% | 96.35% | 92.05% | 97.75% |
| [nibblecode 0.1.0][nibblecode] | 99.94% | † | 100.00% | 96.35% | 92.05% | 99.62% |
| [postcard 1.1.1][postcard] | 30.98% | 11.82% | 100.00% | 96.35% | 92.05% | 98.54% |
| [pot 3.0.1][pot] | 0.38% | 0.21% | 59.27% | 76.05% | 71.83% | 10.30% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*1.91%\**</span> <span title="populate + encode">*1.74%\**</span> | 1.08% | 68.57% | 77.75% | 76.64% | 11.85% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*1.04%\**</span> <span title="populate + encode">*0.48%\**</span> | 0.51% | 68.57% | 77.75% | 76.64% | 10.78% |
| [rkyv 0.8.10][rkyv] | 100.00% | <span title="unvalidated">*97.79%\**</span> <span title="validated upfront with error">*98.66%\**</span> | 100.00% | 96.35% | 92.05% | 97.28% |
| [ron 0.10.1][ron] | 0.09% | 0.03% | 27.04% | 57.77% | 60.48% | 5.42% |
| [savefile 0.18.6][savefile] | 99.75% | 100.00% | 100.00% | 96.35% | 92.05% | 99.02% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 3.10% | 3.65% | 100.00% | 96.35% | 92.05% | 95.86% |
| [serde-brief 0.1.1][serde-brief] | 0.87% | 0.40% | 38.10% | 64.58% | 72.23% | 9.00% |
| [serde_bare 0.5.0][serde_bare] | 2.48% | 3.05% | 100.00% | 96.35% | 92.05% | 97.80% |
| [speedy 0.8.7][speedy] | 99.67% | 99.51% | 100.00% | 96.35% | 92.05% | 99.60% |
| [wincode 0.2.4][wincode] | 98.75% | 99.50% | 100.00% | 96.35% | 92.05% | 99.06% |
| [wiring 0.2.4][wiring] | 99.19% | 43.51% | 100.00% | 96.34% | 92.05% | 99.74% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.11%\**</span> | <span title="validated on-demand with error">*1.90%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 5.68% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*49.92%\**</span> <span title="validated upfront with error">*2.82%\**</span> | <span title="unvalidated">*49.78%\**</span> <span title="validated upfront with error">*49.77%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*79.92%\**</span> | <span title="unvalidated">*99.98%\**</span> <span title="validated upfront with error">*99.98%\**</span> | <span title="unvalidated">*95.76%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*99.95%\**</span> <span title="validated upfront with error">*23.46%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*99.56%\**</span> | <span title="unvalidated">*100.00%\**</span> |

## `minecraft_savedata`

This data set is composed of Minecraft player saves that contain highly structured data.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Borrow | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*878.00 µs\**</span> <span title="prepend">*785.47 µs\**</span> | 3.1305 ms | 1.6952 ms | 489348 | 281173 | 249360 | 2.6235 ms |
| [bin-proto 0.12.3][bin-proto] | 1.9204 ms | 2.8409 ms | † | 566975 | 239350 | 231475 | 2.4934 ms |
| [bincode 2.0.1][bincode] | 318.10 µs | 1.8355 ms | 801.85 µs | 367413 | 221291 | 206242 | 2.0648 ms |
| [bincode 1.3.3][bincode1] | 595.88 µs | 1.8692 ms | 873.32 µs | 569975 | 240525 | 231884 | 2.4536 ms |
| [bitcode 0.6.6][bitcode] | 125.45 µs | 1.2872 ms | 171.77 µs | 327688 | 200947 | 182040 | 763.59 µs |
| [borsh 1.5.7][borsh] | 554.22 µs | 1.8206 ms | † | 446595 | 234236 | 209834 | 2.0953 ms |
| [capnp 0.23.2][capnp] | 448.02 µs | † | † | 803896 | 335606 | 280744 | 3.6126 ms |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 747.91 µs | 4.6368 ms | 3.3846 ms | 1109831 | 344745 | 274333 | 3.6016 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 3.7697 ms | 9.9831 ms | † | 1109821 | 344751 | 274345 | 3.4845 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 1.8896 ms | 4.7873 ms | 3.4399 ms | 1109821 | 344751 | 274345 | 3.5976 ms |
| [columnar 0.11.1][columnar] | 291.60 µs | 1.9328 ms <span title="copy_from">*782.38 µs\**</span> | † | 563728 | 249696 | 217582 | 1.6375 ms |
| [databuf 0.5.0][databuf] | 287.14 µs | 1.7745 ms | 788.93 µs | 356311 | 213062 | 198403 | 2.0034 ms |
| [dlhn 0.1.7][dlhn] | 704.66 µs | 2.6397 ms | † | 366496 | 220600 | 205586 | 2.0261 ms |
| [flatbuffers 25.12.19][flatbuffers] | 3.2720 ms | † | † | 849472 | 347816 | 294871 | 3.6174 ms |
| [flexbuffers 25.2.10][flexbuffers] | 7.8305 ms | 7.4403 ms | 6.1420 ms | 1187688 | 557642 | 553730 | 6.3445 ms |
| json:<br> [flexon 0.4.5][flexon] | 2.8085 ms | 4.6187 ms | † | 1623191 | 466527 | 359157 | 5.7754 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 3.7082 ms | 6.9537 ms | † | 1623191 | 466527 | 359157 | 5.8044 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 2.2044 ms | 4.7850 ms | † | 1623191 | 466527 | 359157 | 5.8601 ms |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 751.21 µs | 2.8705 ms | † | 391251 | 236877 | 220395 | 2.3112 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 1.4705 ms | 3.0213 ms | 1.6706 ms | 424533 | 245214 | 226077 | 2.4020 ms |
| [minicbor 1.0.0][minicbor] | 527.75 µs | 3.3985 ms | 1.9478 ms | 428773 | 249857 | 228630 | 2.3231 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 5.1515 ms | 3.9774 ms | 2.8171 ms | 449745 | 252432 | 230965 | 2.4517 ms |
| [nanoserde 0.2.1][nanoserde] | 270.94 µs | 1.9128 ms | † | 567975 | 239930 | 231872 | 2.5192 ms |
| [nibblecode 0.1.0][nibblecode] | 184.36 µs | † | † | 603928 | 430132 | 406532 | 3.8273 ms |
| [postcard 1.1.1][postcard] | 452.90 µs | 2.0870 ms | 810.42 µs | 367489 | 221913 | 207244 | 2.0839 ms |
| [pot 3.0.1][pot] | 2.4411 ms | 6.1993 ms | 5.1210 ms | 599125 | 299158 | 247675 | 2.7644 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*1.2739 ms\**</span> <span title="populate + encode">*3.0429 ms\**</span> | 3.4718 ms | † | 596811 | 305319 | 268737 | 3.1590 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*1.0452 ms\**</span> <span title="populate + encode">*3.0560 ms\**</span> | 3.8577 ms | † | 596811 | 305319 | 268737 | 3.1178 ms |
| [rkyv 0.8.10][rkyv] | 332.23 µs | <span title="unvalidated">*1.5069 ms\**</span> <span title="validated upfront with error">*1.8587 ms\**</span> | † | 603776 | 254776 | 219421 | 2.3469 ms |
| [ron 0.10.1][ron] | 8.3345 ms | 24.936 ms | 23.551 ms | 1465223 | 434935 | 342907 | 5.7723 ms |
| [savefile 0.18.6][savefile] | 214.56 µs | 1.8197 ms | † | 566991 | 239362 | 231478 | 2.4849 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 624.73 µs | 2.1377 ms | † | 356311 | 212976 | 198423 | 2.0724 ms |
| [serde-brief 0.1.1][serde-brief] | 1.2507 ms | 5.2472 ms | 3.6729 ms | 1276014 | 373898 | 293384 | 3.8034 ms |
| [serde_bare 0.5.0][serde_bare] | 746.42 µs | 2.3568 ms | † | 356311 | 213062 | 198403 | 2.0636 ms |
| [speedy 0.8.7][speedy] | 274.40 µs | 1.6986 ms | 540.82 µs | 449595 | 234970 | 210192 | 2.1124 ms |
| [wincode 0.2.4][wincode] | 204.06 µs | 1.6788 ms | 634.31 µs | 566975 | 239350 | 231475 | 2.5554 ms |
| [wiring 0.2.4][wiring] | 208.51 µs | 1.9277 ms | † | 566975 | 247810 | 225086 | 2.5128 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*80.293 ns\**</span> | <span title="validated on-demand with error">*422.00 ns\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 897.97 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.4935 ns\**</span> <span title="validated upfront with error">*2.1601 ms\**</span> | <span title="unvalidated">*1.4225 µs\**</span> <span title="validated upfront with error">*2.1557 ms\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.2459 ns\**</span> <span title="validated upfront with error">*250.34 µs\**</span> | <span title="unvalidated">*156.34 ns\**</span> <span title="validated upfront with error">*249.19 µs\**</span> | <span title="unvalidated">*737.65 ns\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.2470 ns\**</span> <span title="validated upfront with error">*331.92 µs\**</span> | <span title="unvalidated">*156.79 ns\**</span> <span title="validated upfront with error">*336.92 µs\**</span> | <span title="unvalidated">*727.43 ns\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Borrow | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*14.29%\**</span> <span title="prepend">*15.97%\**</span> | 24.99% | 10.13% | 66.96% | 71.47% | 73.00% | 29.11% |
| [bin-proto 0.12.3][bin-proto] | 6.53% | 27.54% | † | 57.80% | 83.96% | 78.64% | 30.62% |
| [bincode 2.0.1][bincode] | 39.44% | 42.62% | 21.42% | 89.19% | 90.81% | 88.27% | 36.98% |
| [bincode 1.3.3][bincode1] | 21.05% | 41.86% | 19.67% | 57.49% | 83.55% | 78.50% | 31.12% |
| [bitcode 0.6.6][bitcode] | 100.00% | 60.78% | 100.00% | 100.00% | 100.00% | 100.00% | 100.00% |
| [borsh 1.5.7][borsh] | 22.64% | 42.97% | † | 73.37% | 85.79% | 86.75% | 36.44% |
| [capnp 0.23.2][capnp] | 28.00% | † | † | 40.76% | 59.88% | 64.84% | 21.14% |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 16.77% | 16.87% | 5.08% | 29.53% | 58.29% | 66.36% | 21.20% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 3.33% | 7.84% | † | 29.53% | 58.29% | 66.35% | 21.91% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 6.64% | 16.34% | 4.99% | 29.53% | 58.29% | 66.35% | 21.22% |
| [columnar 0.11.1][columnar] | 43.02% | 40.48% <span title="copy_from">*100.00%\**</span> | † | 58.13% | 80.48% | 83.67% | 46.63% |
| [databuf 0.5.0][databuf] | 43.69% | 44.09% | 21.77% | 91.97% | 94.31% | 91.75% | 38.11% |
| [dlhn 0.1.7][dlhn] | 17.80% | 29.64% | † | 89.41% | 91.09% | 88.55% | 37.69% |
| [flatbuffers 25.12.19][flatbuffers] | 3.83% | † | † | 38.58% | 57.77% | 61.74% | 21.11% |
| [flexbuffers 25.2.10][flexbuffers] | 1.60% | 10.52% | 2.80% | 27.59% | 36.04% | 32.88% | 12.04% |
| json:<br> [flexon 0.4.5][flexon] | 4.47% | 16.94% | † | 20.19% | 43.07% | 50.69% | 13.22% |
| json:<br> [serde_json 1.0.140][serde_json] | 3.38% | 11.25% | † | 20.19% | 43.07% | 50.69% | 13.16% |
| json:<br> [simd-json 0.15.1][simd-json] | 5.69% | 16.35% | † | 20.19% | 43.07% | 50.69% | 13.03% |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 16.70% | 27.26% | † | 83.75% | 84.83% | 82.60% | 33.04% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 8.53% | 25.90% | 10.28% | 77.19% | 81.95% | 80.52% | 31.79% |
| [minicbor 1.0.0][minicbor] | 23.77% | 23.02% | 8.82% | 76.42% | 80.42% | 79.62% | 32.87% |
| [nachricht-serde 0.4.0][nachricht-serde] | 2.44% | 19.67% | 6.10% | 72.86% | 79.60% | 78.82% | 31.15% |
| [nanoserde 0.2.1][nanoserde] | 46.30% | 40.90% | † | 57.69% | 83.75% | 78.51% | 30.31% |
| [nibblecode 0.1.0][nibblecode] | 68.05% | † | † | 54.26% | 46.72% | 44.78% | 19.95% |
| [postcard 1.1.1][postcard] | 27.70% | 37.49% | 21.20% | 89.17% | 90.55% | 87.84% | 36.64% |
| [pot 3.0.1][pot] | 5.14% | 12.62% | 3.35% | 54.69% | 67.17% | 73.50% | 27.62% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*9.85%\**</span> <span title="populate + encode">*4.12%\**</span> | 22.54% | † | 54.91% | 65.82% | 67.74% | 24.17% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*12.00%\**</span> <span title="populate + encode">*4.11%\**</span> | 20.28% | † | 54.91% | 65.82% | 67.74% | 24.49% |
| [rkyv 0.8.10][rkyv] | 37.76% | <span title="unvalidated">*51.92%\**</span> <span title="validated upfront with error">*42.09%\**</span> | † | 54.27% | 78.87% | 82.96% | 32.54% |
| [ron 0.10.1][ron] | 1.51% | 3.14% | 0.73% | 22.36% | 46.20% | 53.09% | 13.23% |
| [savefile 0.18.6][savefile] | 58.47% | 42.99% | † | 57.79% | 83.95% | 78.64% | 30.73% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 20.08% | 36.60% | † | 91.97% | 94.35% | 91.74% | 36.85% |
| [serde-brief 0.1.1][serde-brief] | 10.03% | 14.91% | 4.68% | 25.68% | 53.74% | 62.05% | 20.08% |
| [serde_bare 0.5.0][serde_bare] | 16.81% | 33.20% | † | 91.97% | 94.31% | 91.75% | 37.00% |
| [speedy 0.8.7][speedy] | 45.72% | 46.06% | 31.76% | 72.89% | 85.52% | 86.61% | 36.15% |
| [wincode 0.2.4][wincode] | 61.48% | 46.60% | 27.08% | 57.80% | 83.96% | 78.64% | 29.88% |
| [wiring 0.2.4][wiring] | 60.16% | 40.59% | † | 57.80% | 81.09% | 80.88% | 30.39% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.55%\**</span> | <span title="validated on-demand with error">*37.05%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 0.14% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*49.97%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*10.99%\**</span> <span title="validated upfront with error">*0.01%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.06%\**</span> | <span title="unvalidated">*98.61%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*99.91%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*99.71%\**</span> <span title="validated upfront with error">*0.05%\**</span> | <span title="unvalidated">*100.00%\**</span> |

## `mk48`

This data set is composed of mk48.io game updates that contain data with many exploitable patterns and invariants.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*4.6165 ms\**</span> <span title="prepend">*2.5467 ms\**</span> | 8.8078 ms | 1704643 | 1294259 | 1245668 | 11.992 ms |
| [bin-proto 0.12.3][bin-proto] | 5.7882 ms | 6.6166 ms | 1791489 | 1127998 | 1051146 | 10.828 ms |
| [bincode 2.0.1][bincode] | 1.4785 ms | 3.6762 ms | 1406257 | 1117802 | 1062438 | 10.147 ms |
| [bincode 1.3.3][bincode1] | 3.9663 ms | 4.3743 ms | 1854234 | 1141994 | 1048745 | 10.686 ms |
| [bitcode 0.6.6][bitcode] | 693.89 µs | 2.3851 ms | 971318 | 878034 | 850340 | 2.9498 ms |
| [borsh 1.5.7][borsh] | 2.7955 ms | 2.9077 ms | 1521989 | 1108471 | 1038528 | 10.199 ms |
| [capnp 0.23.2][capnp] | 2.1639 ms | † | 2724288 | 1546992 | 1239111 | 15.220 ms |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 3.2540 ms | 18.404 ms | 6012539 | 1695215 | 1464951 | 21.464 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 23.969 ms | 53.352 ms | 6012373 | 1695146 | 1465025 | 21.783 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 9.9137 ms | 20.885 ms | 6012373 | 1695146 | 1465025 | 21.935 ms |
| [columnar 0.11.1][columnar] | 901.98 µs | 3.7716 ms <span title="copy_from">*1.2749 ms\**</span> | 1544752 | 996728 | 897073 | 4.8486 ms |
| [databuf 0.5.0][databuf] | 1.3255 ms | 3.7977 ms | 1319999 | 1062631 | 1008334 | 9.2099 ms |
| [dlhn 0.1.7][dlhn] | 4.6255 ms | 7.9764 ms | 1311281 | 1077520 | 1046095 | 8.9393 ms |
| [flatbuffers 25.12.19][flatbuffers] | 5.0119 ms | † | 2325620 | 1439185 | 1268060 | 14.209 ms |
| [flexbuffers 25.2.10][flexbuffers] | 39.681 ms | 37.157 ms | 5352680 | 2658295 | 2777967 | 35.803 ms |
| json:<br> [flexon 0.4.5][flexon] | 15.174 ms | 25.790 ms | 9390461 | 2391679 | 1842767 | 35.786 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 20.443 ms | 31.857 ms | 9390461 | 2391679 | 1842767 | 35.456 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 12.075 ms | 25.271 ms | 9390461 | 2391679 | 1842767 | 35.603 ms |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 1.7874 ms | 6.3068 ms | 1458773 | 1156055 | 1137788 | 10.253 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 10.186 ms | 10.964 ms | 1745322 | 1261627 | 1228923 | 11.996 ms |
| [minicbor 1.0.0][minicbor] | 2.0703 ms | 11.820 ms | 1777386 | 1276218 | 1252558 | 12.895 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 30.352 ms | 17.092 ms | 1770060 | 1277755 | 1263362 | 13.051 ms |
| [nanoserde 0.2.1][nanoserde] | 1.2887 ms | 2.7798 ms | 1812404 | 1134820 | 1053109 | 10.655 ms |
| [nibblecode 0.1.0][nibblecode] | 511.19 µs | † | 2075936 | 1503435 | 1396519 | 14.467 ms |
| [postcard 1.1.1][postcard] | 1.8900 ms | 4.2753 ms | 1311281 | 1083900 | 1041434 | 9.0516 ms |
| [pot 3.0.1][pot] | 14.302 ms | 30.268 ms | 2604812 | 1482233 | 1298928 | 16.403 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*5.5039 ms\**</span> <span title="populate + encode">*9.7334 ms\**</span> | 9.1375 ms | 1859886 | 1338076 | 1295351 | 12.794 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*5.6730 ms\**</span> <span title="populate + encode">*13.657 ms\**</span> | 13.612 ms | 1859886 | 1338076 | 1295351 | 12.664 ms |
| [rkyv 0.8.10][rkyv] | 991.37 µs | <span title="unvalidated">*2.2475 ms\**</span> <span title="validated upfront with error">*2.6705 ms\**</span> | 2075936 | 1383779 | 1210377 | 13.332 ms |
| [ron 0.10.1][ron] | 43.645 ms | 151.86 ms | 8677703 | 2233642 | 1826180 | 40.190 ms |
| [savefile 0.18.6][savefile] | 866.46 µs | 2.5960 ms | 1791505 | 1128012 | 1051153 | 10.220 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 3.1301 ms | 3.5804 ms | 1319999 | 1064380 | 1010708 | 9.0582 ms |
| [serde-brief 0.1.1][serde-brief] | 6.2580 ms | 22.892 ms | 6951772 | 1796265 | 1567819 | 24.361 ms |
| [serde_bare 0.5.0][serde_bare] | 4.9002 ms | 5.0851 ms | 1319999 | 1062645 | 1008349 | 8.9275 ms |
| [speedy 0.8.7][speedy] | 780.14 µs | 2.4688 ms | 1584734 | 1119837 | 1037992 | 10.222 ms |
| [wincode 0.2.4][wincode] | 581.19 µs | 2.4007 ms | 1791489 | 1127998 | 1051146 | 10.458 ms |
| [wiring 0.2.4][wiring] | 645.10 µs | 2.7583 ms | 1791489 | 1156963 | 1082815 | 10.601 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*83.038 ns\**</span> | <span title="validated on-demand with error">*720.58 ns\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 58.263 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.4930 ns\**</span> <span title="validated upfront with error">*5.9691 ms\**</span> | <span title="unvalidated">*2.7407 µs\**</span> <span title="validated upfront with error">*5.9320 ms\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.2464 ns\**</span> <span title="validated upfront with error">*344.94 µs\**</span> | <span title="unvalidated">*377.96 ns\**</span> <span title="validated upfront with error">*345.19 µs\**</span> | <span title="unvalidated">*239.01 ns\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.2454 ns\**</span> <span title="validated upfront with error">*417.26 µs\**</span> | <span title="unvalidated">*385.63 ns\**</span> <span title="validated upfront with error">*418.30 µs\**</span> | <span title="unvalidated">*235.72 ns\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*11.07%\**</span> <span title="prepend">*20.07%\**</span> | 14.47% | 56.98% | 67.84% | 68.26% | 24.60% |
| [bin-proto 0.12.3][bin-proto] | 8.83% | 19.27% | 54.22% | 77.84% | 80.90% | 27.24% |
| [bincode 2.0.1][bincode] | 34.57% | 34.68% | 69.07% | 78.55% | 80.04% | 29.07% |
| [bincode 1.3.3][bincode1] | 12.89% | 29.15% | 52.38% | 76.89% | 81.08% | 27.60% |
| [bitcode 0.6.6][bitcode] | 73.67% | 53.45% | 100.00% | 100.00% | 100.00% | 100.00% |
| [borsh 1.5.7][borsh] | 18.29% | 43.85% | 63.82% | 79.21% | 81.88% | 28.92% |
| [capnp 0.23.2][capnp] | 23.62% | † | 35.65% | 56.76% | 68.63% | 19.38% |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 15.71% | 6.93% | 16.15% | 51.79% | 58.05% | 13.74% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 2.13% | 2.39% | 16.16% | 51.80% | 58.04% | 13.54% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 5.16% | 6.10% | 16.16% | 51.80% | 58.04% | 13.45% |
| [columnar 0.11.1][columnar] | 56.67% | 33.80% <span title="copy_from">*100.00%\**</span> | 62.88% | 88.09% | 94.79% | 60.84% |
| [databuf 0.5.0][databuf] | 38.57% | 33.57% | 73.58% | 82.63% | 84.33% | 32.03% |
| [dlhn 0.1.7][dlhn] | 11.05% | 15.98% | 74.07% | 81.49% | 81.29% | 33.00% |
| [flatbuffers 25.12.19][flatbuffers] | 10.20% | † | 41.77% | 61.01% | 67.06% | 20.76% |
| [flexbuffers 25.2.10][flexbuffers] | 1.29% | 3.43% | 18.15% | 33.03% | 30.61% | 8.24% |
| json:<br> [flexon 0.4.5][flexon] | 3.37% | 4.94% | 10.34% | 36.71% | 46.14% | 8.24% |
| json:<br> [serde_json 1.0.140][serde_json] | 2.50% | 4.00% | 10.34% | 36.71% | 46.14% | 8.32% |
| json:<br> [simd-json 0.15.1][simd-json] | 4.23% | 5.04% | 10.34% | 36.71% | 46.14% | 8.29% |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 28.60% | 20.21% | 66.58% | 75.95% | 74.74% | 28.77% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 5.02% | 11.63% | 55.65% | 69.60% | 69.19% | 24.59% |
| [minicbor 1.0.0][minicbor] | 24.69% | 10.79% | 54.65% | 68.80% | 67.89% | 22.88% |
| [nachricht-serde 0.4.0][nachricht-serde] | 1.68% | 7.46% | 54.87% | 68.72% | 67.31% | 22.60% |
| [nanoserde 0.2.1][nanoserde] | 39.67% | 45.86% | 53.59% | 77.37% | 80.75% | 27.68% |
| [nibblecode 0.1.0][nibblecode] | 100.00% | † | 46.79% | 58.40% | 60.89% | 20.39% |
| [postcard 1.1.1][postcard] | 27.05% | 29.82% | 74.07% | 81.01% | 81.65% | 32.59% |
| [pot 3.0.1][pot] | 3.57% | 4.21% | 37.29% | 59.24% | 65.46% | 17.98% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*9.29%\**</span> <span title="populate + encode">*5.25%\**</span> | 13.95% | 52.22% | 65.62% | 65.65% | 23.06% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*9.01%\**</span> <span title="populate + encode">*3.74%\**</span> | 9.37% | 52.22% | 65.62% | 65.65% | 23.29% |
| [rkyv 0.8.10][rkyv] | 51.56% | <span title="unvalidated">*56.73%\**</span> <span title="validated upfront with error">*47.74%\**</span> | 46.79% | 63.45% | 70.25% | 22.13% |
| [ron 0.10.1][ron] | 1.17% | 0.84% | 11.19% | 39.31% | 46.56% | 7.34% |
| [savefile 0.18.6][savefile] | 59.00% | 49.11% | 54.22% | 77.84% | 80.90% | 28.86% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 16.33% | 35.61% | 73.58% | 82.49% | 84.13% | 32.56% |
| [serde-brief 0.1.1][serde-brief] | 8.17% | 5.57% | 13.97% | 48.88% | 54.24% | 12.11% |
| [serde_bare 0.5.0][serde_bare] | 10.43% | 25.07% | 73.58% | 82.63% | 84.33% | 33.04% |
| [speedy 0.8.7][speedy] | 65.53% | 51.64% | 61.29% | 78.41% | 81.92% | 28.86% |
| [wincode 0.2.4][wincode] | 87.96% | 53.11% | 54.22% | 77.84% | 80.90% | 28.21% |
| [wiring 0.2.4][wiring] | 79.24% | 46.22% | 54.22% | 75.89% | 78.53% | 27.83% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.50%\**</span> | <span title="validated on-demand with error">*52.45%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 2.14% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*49.96%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*13.79%\**</span> <span title="validated upfront with error">*0.01%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*99.92%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.11%\**</span> | <span title="unvalidated">*98.62%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*98.01%\**</span> <span title="validated upfront with error">*0.09%\**</span> | <span title="unvalidated">*100.00%\**</span> |

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


## Footnotes:

\* *mouse over for situational details*

† *this deserialization capability is not supported*

‡ *buffer mutation is not supported (`capnp` and `flatbuffers` may but not for rust)*
