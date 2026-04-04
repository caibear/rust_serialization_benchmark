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

## Last updated: 2026-04-03 23:13:51

<details><summary>Runtime info</summary>

### `rustc` version

```
rustc 1.96.0-nightly (55e86c996 2026-04-02)
binary: rustc
commit-hash: 55e86c996809902e8bbad512cfb4d2c18be446d9
commit-date: 2026-04-02
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
Model name:                              AMD EPYC 9V74 80-Core Processor
CPU family:                              25
Model:                                   17
Thread(s) per core:                      2
Core(s) per socket:                      2
Socket(s):                               1
Stepping:                                1
BogoMIPS:                                5192.30
Flags:                                   fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ht syscall nx mmxext fxsr_opt pdpe1gb rdtscp lm constant_tsc rep_good nopl tsc_reliable nonstop_tsc cpuid extd_apicid aperfmperf tsc_known_freq pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 movbe popcnt aes xsave avx f16c rdrand hypervisor lahf_lm cmp_legacy svm cr8_legacy abm sse4a misalignsse 3dnowprefetch osvw topoext vmmcall fsgsbase bmi1 avx2 smep bmi2 erms invpcid rdseed adx smap clflushopt clwb sha_ni xsaveopt xsavec xgetbv1 xsaves user_shstk clzero xsaveerptr rdpru arat npt nrip_save tsc_scale vmcb_clean flushbyasid decodeassists pausefilter pfthreshold v_vmsave_vmload umip vaes vpclmulqdq rdpid fsrm
Virtualization:                          AMD-V
Hypervisor vendor:                       Microsoft
Virtualization type:                     full
L1d cache:                               64 KiB (2 instances)
L1i cache:                               64 KiB (2 instances)
L2 cache:                                2 MiB (2 instances)
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
| [bilrost 0.1013.0][bilrost] | <span title="encode">*403.54 µs\**</span> <span title="prepend">*332.39 µs\**</span> | 2.6597 ms | 886.36 µs | 804955 | 328941 | 284849 | 5.0966 ms |
| [bin-proto 0.12.3][bin-proto] | 4.9546 ms | 4.6836 ms | † | 1045784 | 373127 | 311553 | 4.3334 ms |
| [bincode 2.0.1][bincode] | 342.95 µs | 2.2273 ms | 684.97 µs | 741295 | 303944 | 256422 | 3.4918 ms |
| [bincode 1.3.3][bincode1] | 596.87 µs | 2.0901 ms | 611.19 µs | 1045784 | 373127 | 311553 | 4.3581 ms |
| [bitcode 0.6.6][bitcode] | 121.30 µs | 1.4712 ms | 63.989 µs | 703710 | 288826 | 227322 | 2.4657 ms |
| [borsh 1.5.7][borsh] | 573.97 µs | 2.1916 ms | † | 885780 | 362204 | 286248 | 3.9997 ms |
| [capnp 0.23.2][capnp] | 510.72 µs | † | † | 1443216 | 513986 | 426532 | 6.1047 ms |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 524.30 µs | 5.1759 ms | 3.5742 ms | 1407835 | 403440 | 323561 | 4.8988 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 3.2666 ms | 13.358 ms | † | 1407835 | 403440 | 323561 | 4.9179 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 2.0501 ms | 4.5735 ms | 2.9779 ms | 1407835 | 403440 | 323561 | 4.9305 ms |
| [columnar 0.11.1][columnar] | 231.11 µs | 2.2531 ms <span title="copy_from">*886.18 µs\**</span> | † | 1045928 | 370212 | 293907 | 3.8578 ms |
| [databuf 0.5.0][databuf] | 266.31 µs | 2.1129 ms | 719.66 µs | 765778 | 311715 | 263914 | 3.2207 ms |
| [dlhn 0.1.7][dlhn] | 730.58 µs | 2.5636 ms | † | 724953 | 301446 | 253056 | 2.9266 ms |
| [flatbuffers 25.12.19][flatbuffers] | 964.76 µs | † | † | 1276368 | 468539 | 388381 | 4.5328 ms |
| [flexbuffers 25.2.10][flexbuffers] | 6.9071 ms | 7.4346 ms | 5.7920 ms | 1829756 | 714318 | 691541 | 7.8909 ms |
| json:<br> [flexon 0.4.5][flexon] | 2.4439 ms | 3.8344 ms | † | 1827461 | 470560 | 360727 | 5.4122 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 4.1113 ms | 6.1075 ms | † | 1827461 | 470560 | 360727 | 5.7544 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 2.2666 ms | 4.7894 ms | † | 1827461 | 470560 | 360727 | 5.3947 ms |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 1.1420 ms | 2.6980 ms | † | 764996 | 315291 | 264212 | 3.3598 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 1.5252 ms | 2.9982 ms | 1.3396 ms | 784997 | 325384 | 277608 | 3.5119 ms |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 299.40 µs | 2.5934 ms | 853.88 µs | 784997 | 325384 | 277608 | 3.4696 ms |
| [minicbor 1.0.0][minicbor] | 491.75 µs | 3.0546 ms | 1.3732 ms | 817830 | 332671 | 284034 | 3.7776 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 5.6027 ms | 4.1210 ms | 2.6548 ms | 818669 | 332556 | 284797 | 3.8593 ms |
| [nanoserde 0.2.1][nanoserde] | 233.06 µs | 2.1678 ms | † | 1045784 | 373127 | 311553 | 3.8935 ms |
| [nibblecode 0.1.0][nibblecode] | 184.67 µs | † | † | 1011487 | 473998 | 404660 | 4.9161 ms |
| [postcard 1.1.1][postcard] | 471.58 µs | 2.3907 ms | 794.86 µs | 724953 | 302399 | 252968 | 3.1004 ms |
| [pot 3.0.1][pot] | 2.4292 ms | 6.3285 ms | 4.9231 ms | 971922 | 372513 | 303636 | 4.1131 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*935.21 µs\**</span> <span title="populate + encode">*2.4782 ms\**</span> | 3.5127 ms | † | 884628 | 363130 | 314959 | 4.0521 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*1.3340 ms\**</span> <span title="populate + encode">*3.2396 ms\**</span> | 4.1201 ms | † | 884628 | 363130 | 314959 | 4.0422 ms |
| [rkyv 0.8.10][rkyv] | 235.00 µs | <span title="unvalidated">*1.5753 ms\**</span> <span title="validated upfront with error">*1.9472 ms\**</span> | † | 1011488 | 393526 | 325965 | 4.3334 ms |
| [ron 0.10.1][ron] | 10.940 ms | 25.139 ms | 22.813 ms | 1607459 | 449158 | 349324 | 5.4128 ms |
| [savefile 0.18.6][savefile] | 180.65 µs | 2.1524 ms | † | 1045800 | 373139 | 311562 | 4.0327 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 695.43 µs | 2.4555 ms | † | 765778 | 311743 | 263822 | 3.3402 ms |
| [serde-brief 0.1.1][serde-brief] | 1.4200 ms | 4.8689 ms | 2.9598 ms | 1584946 | 413733 | 339964 | 4.6807 ms |
| [serde_bare 0.5.0][serde_bare] | 759.14 µs | 2.1430 ms | † | 765778 | 311715 | 263914 | 3.2111 ms |
| [speedy 0.8.7][speedy] | 192.58 µs | 1.8124 ms | 390.77 µs | 885780 | 362204 | 286248 | 3.6422 ms |
| [wincode 0.2.4][wincode] | 163.85 µs | 1.9988 ms | 478.75 µs | 1045784 | 373127 | 311553 | 3.9438 ms |
| [wiring 0.2.4][wiring] | 175.32 µs | 2.1260 ms | † | 1045784 | 337930 | 275808 | 3.4592 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*92.594 ns\**</span> | <span title="validated on-demand with error">*131.61 µs\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 22.061 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.8121 ns\**</span> <span title="validated upfront with error">*2.6048 ms\**</span> | <span title="unvalidated">*55.731 µs\**</span> <span title="validated upfront with error">*2.6498 ms\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.4062 ns\**</span> <span title="validated upfront with error">*96.988 µs\**</span> | <span title="unvalidated">*10.745 µs\**</span> <span title="validated upfront with error">*107.98 µs\**</span> | <span title="unvalidated">*6.2713 µs\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.4060 ns\**</span> <span title="validated upfront with error">*342.05 µs\**</span> | <span title="unvalidated">*10.747 µs\**</span> <span title="validated upfront with error">*357.90 µs\**</span> | <span title="unvalidated">*6.2285 µs\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Borrow | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*30.06%\**</span> <span title="prepend">*36.49%\**</span> | 33.32% | 7.22% | 87.42% | 87.80% | 79.80% | 48.38% |
| [bin-proto 0.12.3][bin-proto] | 2.45% | 18.92% | † | 67.29% | 77.41% | 72.96% | 56.90% |
| [bincode 2.0.1][bincode] | 35.37% | 39.79% | 9.34% | 94.93% | 95.03% | 88.65% | 70.61% |
| [bincode 1.3.3][bincode1] | 20.32% | 42.40% | 10.47% | 67.29% | 77.41% | 72.96% | 56.58% |
| [bitcode 0.6.6][bitcode] | 100.00% | 60.24% | 100.00% | 100.00% | 100.00% | 100.00% | 100.00% |
| [borsh 1.5.7][borsh] | 21.13% | 40.44% | † | 79.45% | 79.74% | 79.41% | 61.65% |
| [capnp 0.23.2][capnp] | 23.75% | † | † | 48.76% | 56.19% | 53.30% | 40.39% |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 23.14% | 17.12% | 1.79% | 49.99% | 71.59% | 70.26% | 50.33% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 3.71% | 6.63% | † | 49.99% | 71.59% | 70.26% | 50.14% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 5.92% | 19.38% | 2.15% | 49.99% | 71.59% | 70.26% | 50.01% |
| [columnar 0.11.1][columnar] | 52.49% | 39.33% <span title="copy_from">*100.00%\**</span> | † | 67.28% | 78.02% | 77.34% | 63.91% |
| [databuf 0.5.0][databuf] | 45.55% | 41.94% | 8.89% | 91.89% | 92.66% | 86.13% | 76.56% |
| [dlhn 0.1.7][dlhn] | 16.60% | 34.57% | † | 97.07% | 95.81% | 89.83% | 84.25% |
| [flatbuffers 25.12.19][flatbuffers] | 12.57% | † | † | 55.13% | 61.64% | 58.53% | 54.40% |
| [flexbuffers 25.2.10][flexbuffers] | 1.76% | 11.92% | 1.10% | 38.46% | 40.43% | 32.87% | 31.25% |
| json:<br> [flexon 0.4.5][flexon] | 4.96% | 23.11% | † | 38.51% | 61.38% | 63.02% | 45.56% |
| json:<br> [serde_json 1.0.140][serde_json] | 2.95% | 14.51% | † | 38.51% | 61.38% | 63.02% | 42.85% |
| json:<br> [simd-json 0.15.1][simd-json] | 5.35% | 18.50% | † | 38.51% | 61.38% | 63.02% | 45.71% |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 10.62% | 32.85% | † | 91.99% | 91.61% | 86.04% | 73.39% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 7.95% | 29.56% | 4.78% | 89.64% | 88.76% | 81.89% | 70.21% |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 40.51% | 34.17% | 7.49% | 89.64% | 88.76% | 81.89% | 71.07% |
| [minicbor 1.0.0][minicbor] | 24.67% | 29.01% | 4.66% | 86.05% | 86.82% | 80.03% | 65.27% |
| [nachricht-serde 0.4.0][nachricht-serde] | 2.17% | 21.50% | 2.41% | 85.96% | 86.85% | 79.82% | 63.89% |
| [nanoserde 0.2.1][nanoserde] | 52.05% | 40.88% | † | 67.29% | 77.41% | 72.96% | 63.33% |
| [nibblecode 0.1.0][nibblecode] | 65.68% | † | † | 69.57% | 60.93% | 56.18% | 50.16% |
| [postcard 1.1.1][postcard] | 25.72% | 37.07% | 8.05% | 97.07% | 95.51% | 89.86% | 79.53% |
| [pot 3.0.1][pot] | 4.99% | 14.00% | 1.30% | 72.40% | 77.53% | 74.87% | 59.95% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*12.97%\**</span> <span title="populate + encode">*4.89%\**</span> | 25.23% | † | 79.55% | 79.54% | 72.18% | 60.85% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*9.09%\**</span> <span title="populate + encode">*3.74%\**</span> | 21.51% | † | 79.55% | 79.54% | 72.18% | 61.00% |
| [rkyv 0.8.10][rkyv] | 51.62% | <span title="unvalidated">*56.25%\**</span> <span title="validated upfront with error">*45.51%\**</span> | † | 69.57% | 73.39% | 69.74% | 56.90% |
| [ron 0.10.1][ron] | 1.11% | 3.53% | 0.28% | 43.78% | 64.30% | 65.07% | 45.55% |
| [savefile 0.18.6][savefile] | 67.15% | 41.17% | † | 67.29% | 77.40% | 72.96% | 61.14% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 17.44% | 36.09% | † | 91.89% | 92.65% | 86.16% | 73.82% |
| [serde-brief 0.1.1][serde-brief] | 8.54% | 18.20% | 2.16% | 44.40% | 69.81% | 66.87% | 52.68% |
| [serde_bare 0.5.0][serde_bare] | 15.98% | 41.35% | † | 91.89% | 92.66% | 86.13% | 76.79% |
| [speedy 0.8.7][speedy] | 62.99% | 48.90% | 16.38% | 79.45% | 79.74% | 79.41% | 67.70% |
| [wincode 0.2.4][wincode] | 74.03% | 44.34% | 13.37% | 67.29% | 77.41% | 72.96% | 62.52% |
| [wiring 0.2.4][wiring] | 69.19% | 41.68% | † | 67.29% | 85.47% | 82.42% | 71.28% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.52%\**</span> | <span title="validated on-demand with error">*8.16%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 6.37% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*50.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*19.28%\**</span> <span title="validated upfront with error">*0.41%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*99.99%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*9.95%\**</span> | <span title="unvalidated">*99.32%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*99.98%\**</span> <span title="validated upfront with error">*3.00%\**</span> | <span title="unvalidated">*100.00%\**</span> |

## `mesh`

This data set is a single mesh. The mesh contains an array of triangles, each of which has three vertices and a normal vector.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*5.2658 ms\**</span> <span title="prepend">*5.3260 ms\**</span> | 7.4585 ms | 8625005 | 6443961 | 6231572 | 69.326 ms |
| [bin-proto 0.12.3][bin-proto] | 8.9168 ms | 10.038 ms | 6000008 | 5378500 | 5346908 | 9.3119 ms |
| [bincode 2.0.1][bincode] | 1.6802 ms | 1.1622 ms | 6000005 | 5378497 | 5346882 | 9.4253 ms |
| [bincode 1.3.3][bincode1] | 5.9591 ms | 961.84 µs | 6000008 | 5378500 | 5346908 | 9.3813 ms |
| [bitcode 0.6.6][bitcode] | 1.0904 ms | 917.84 µs | 6000006 | 5182295 | 4921841 | 14.037 ms |
| [borsh 1.5.7][borsh] | 6.4871 ms | 4.8077 ms | 6000004 | 5378496 | 5346866 | 9.1683 ms |
| [capnp 0.23.2][capnp] | 5.6972 ms | † | 14000088 | 7130367 | 6046182 | 74.228 ms |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 6.1549 ms | 53.599 ms | 13125016 | 7524114 | 6757437 | 83.488 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 71.432 ms | 132.50 ms | 13122324 | 7524660 | 6759128 | 83.896 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 35.452 ms | 36.814 ms | 13122324 | 7524660 | 6759128 | 84.048 ms |
| [columnar 0.11.1][columnar] | 1.4120 ms | 1.5929 ms <span title="copy_from">*692.27 µs\**</span> | 6000120 | 5378435 | 5347039 | 9.1930 ms |
| [databuf 0.5.0][databuf] | 1.1550 ms | 6.3564 ms | 6000003 | 5378495 | 5346897 | 9.3553 ms |
| [dlhn 0.1.7][dlhn] | 6.3455 ms | 8.0487 ms | 6000003 | 5378495 | 5346897 | 9.2891 ms |
| [flatbuffers 25.12.19][flatbuffers] | 470.70 µs | † | 6000024 | 5378434 | 5346878 | 9.3897 ms |
| [flexbuffers 25.2.10][flexbuffers] | 107.80 ms | 97.012 ms | 26609424 | 11901040 | 12486322 | 141.46 ms |
| json:<br> [flexon 0.4.5][flexon] | 77.749 ms | 56.103 ms | 26192883 | 9566084 | 8584671 | 152.30 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 92.485 ms | 104.08 ms | 26192883 | 9566084 | 8584671 | 152.05 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 58.279 ms | 66.395 ms | 26192883 | 9566084 | 8584671 | 152.35 ms |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 1.5800 ms | 5.9193 ms | 7500005 | 6058442 | 6014500 | 11.282 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 18.750 ms | 16.381 ms | 8125006 | 6494876 | 6391037 | 68.921 ms |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 828.72 µs | 5.0540 ms | 8125006 | 6494876 | 6391037 | 69.541 ms |
| [minicbor 1.0.0][minicbor] | 3.0068 ms | 12.111 ms | 8125006 | 6494907 | 6390894 | 63.787 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 127.53 ms | 28.640 ms | 8125037 | 6493484 | 6386940 | 67.850 ms |
| [nanoserde 0.2.1][nanoserde] | 1.7456 ms | 946.41 µs | 6000008 | 5378500 | 5346908 | 9.3337 ms |
| [nibblecode 0.1.0][nibblecode] | 179.72 µs | † | 6000008 | 5378500 | 5346908 | 9.2672 ms |
| [postcard 1.1.1][postcard] | 533.04 µs | 1.1339 ms | 6000003 | 5378495 | 5346897 | 9.3013 ms |
| [pot 3.0.1][pot] | 39.981 ms | 69.258 ms | 10122342 | 6814618 | 6852252 | 73.731 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*7.0195 ms\**</span> <span title="populate + encode">*7.5017 ms\**</span> | 11.300 ms | 8750000 | 6665735 | 6421877 | 64.795 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*16.090 ms\**</span> <span title="populate + encode">*33.061 ms\**</span> | 32.109 ms | 8750000 | 6665735 | 6421877 | 72.798 ms |
| [rkyv 0.8.10][rkyv] | 179.71 µs | <span title="unvalidated">*178.17 µs\**</span> <span title="validated upfront with error">*178.22 µs\**</span> | 6000008 | 5378500 | 5346872 | 9.1350 ms |
| [ron 0.10.1][ron] | 173.04 ms | 528.95 ms | 22192885 | 8970395 | 8137334 | 145.35 ms |
| [savefile 0.18.6][savefile] | 179.67 µs | 180.21 µs | 6000024 | 5378519 | 5346896 | 9.4669 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 5.2509 ms | 4.8016 ms | 6000004 | 5378496 | 5346866 | 9.1970 ms |
| [serde-brief 0.1.1][serde-brief] | 14.566 ms | 45.264 ms | 15750015 | 8024540 | 6813667 | 87.361 ms |
| [serde_bare 0.5.0][serde_bare] | 5.3389 ms | 5.5444 ms | 6000003 | 5378495 | 5346897 | 9.4384 ms |
| [speedy 0.8.7][speedy] | 179.70 µs | 177.56 µs | 6000004 | 5378496 | 5346866 | 9.1789 ms |
| [wincode 0.2.4][wincode] | 188.16 µs | 184.05 µs | 6000008 | 5378500 | 5346908 | 9.3653 ms |
| [wiring 0.2.4][wiring] | 187.25 µs | 352.90 µs | 6000008 | 5378952 | 5346905 | 9.3766 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*133.16 ns\**</span> | <span title="validated on-demand with error">*2.0052 ms\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 21.135 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.8129 ns\**</span> <span title="validated upfront with error">*51.730 ns\**</span> | <span title="unvalidated">*88.166 µs\**</span> <span title="validated upfront with error">*87.945 µs\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.4066 ns\**</span> <span title="validated upfront with error">*1.5863 ns\**</span> | <span title="unvalidated">*43.957 µs\**</span> <span title="validated upfront with error">*43.944 µs\**</span> | <span title="unvalidated">*98.007 µs\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.4065 ns\**</span> <span title="validated upfront with error">*5.9677 ns\**</span> | <span title="unvalidated">*43.959 µs\**</span> <span title="validated upfront with error">*43.986 µs\**</span> | <span title="unvalidated">*89.522 µs\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*3.41%\**</span> <span title="prepend">*3.37%\**</span> | 2.38% | 69.57% | 80.42% | 78.98% | 13.18% |
| [bin-proto 0.12.3][bin-proto] | 2.01% | 1.77% | 100.00% | 96.35% | 92.05% | 98.10% |
| [bincode 2.0.1][bincode] | 10.69% | 15.28% | 100.00% | 96.35% | 92.05% | 96.92% |
| [bincode 1.3.3][bincode1] | 3.02% | 18.46% | 100.00% | 96.35% | 92.05% | 97.37% |
| [bitcode 0.6.6][bitcode] | 16.48% | 19.35% | 100.00% | 100.00% | 100.00% | 65.08% |
| [borsh 1.5.7][borsh] | 2.77% | 3.69% | 100.00% | 96.35% | 92.05% | 99.64% |
| [capnp 0.23.2][capnp] | 3.15% | † | 42.86% | 72.68% | 81.40% | 12.31% |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 2.92% | 0.33% | 45.71% | 68.88% | 72.84% | 10.94% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 0.25% | 0.13% | 45.72% | 68.87% | 72.82% | 10.89% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 0.51% | 0.48% | 45.72% | 68.87% | 72.82% | 10.87% |
| [columnar 0.11.1][columnar] | 12.72% | 11.15% <span title="copy_from">*25.65%\**</span> | 100.00% | 96.35% | 92.05% | 99.37% |
| [databuf 0.5.0][databuf] | 15.56% | 2.79% | 100.00% | 96.35% | 92.05% | 97.65% |
| [dlhn 0.1.7][dlhn] | 2.83% | 2.21% | 100.00% | 96.35% | 92.05% | 98.34% |
| [flatbuffers 25.12.19][flatbuffers] | 38.17% | † | 100.00% | 96.35% | 92.05% | 97.29% |
| [flexbuffers 25.2.10][flexbuffers] | 0.17% | 0.18% | 22.55% | 43.54% | 39.42% | 6.46% |
| json:<br> [flexon 0.4.5][flexon] | 0.23% | 0.32% | 22.91% | 54.17% | 57.33% | 6.00% |
| json:<br> [serde_json 1.0.140][serde_json] | 0.19% | 0.17% | 22.91% | 54.17% | 57.33% | 6.01% |
| json:<br> [simd-json 0.15.1][simd-json] | 0.31% | 0.27% | 22.91% | 54.17% | 57.33% | 6.00% |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 11.37% | 3.00% | 80.00% | 85.54% | 81.83% | 80.97% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 0.96% | 1.08% | 73.85% | 79.79% | 77.01% | 13.25% |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 21.68% | 3.51% | 73.85% | 79.79% | 77.01% | 13.14% |
| [minicbor 1.0.0][minicbor] | 5.98% | 1.47% | 73.85% | 79.79% | 77.01% | 14.32% |
| [nachricht-serde 0.4.0][nachricht-serde] | 0.14% | 0.62% | 73.85% | 79.81% | 77.06% | 13.46% |
| [nanoserde 0.2.1][nanoserde] | 10.29% | 18.76% | 100.00% | 96.35% | 92.05% | 97.87% |
| [nibblecode 0.1.0][nibblecode] | 99.97% | † | 100.00% | 96.35% | 92.05% | 98.57% |
| [postcard 1.1.1][postcard] | 33.71% | 15.66% | 100.00% | 96.35% | 92.05% | 98.21% |
| [pot 3.0.1][pot] | 0.45% | 0.26% | 59.27% | 76.05% | 71.83% | 12.39% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*2.56%\**</span> <span title="populate + encode">*2.40%\**</span> | 1.57% | 68.57% | 77.75% | 76.64% | 14.10% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*1.12%\**</span> <span title="populate + encode">*0.54%\**</span> | 0.55% | 68.57% | 77.75% | 76.64% | 12.55% |
| [rkyv 0.8.10][rkyv] | 99.98% | <span title="unvalidated">*99.66%\**</span> <span title="validated upfront with error">*99.63%\**</span> | 100.00% | 96.35% | 92.05% | 100.00% |
| [ron 0.10.1][ron] | 0.10% | 0.03% | 27.04% | 57.77% | 60.48% | 6.28% |
| [savefile 0.18.6][savefile] | 100.00% | 98.53% | 100.00% | 96.35% | 92.05% | 96.49% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 3.42% | 3.70% | 100.00% | 96.35% | 92.05% | 99.33% |
| [serde-brief 0.1.1][serde-brief] | 1.23% | 0.39% | 38.10% | 64.58% | 72.23% | 10.46% |
| [serde_bare 0.5.0][serde_bare] | 3.37% | 3.20% | 100.00% | 96.35% | 92.05% | 96.79% |
| [speedy 0.8.7][speedy] | 99.98% | 100.00% | 100.00% | 96.35% | 92.05% | 99.52% |
| [wincode 0.2.4][wincode] | 95.49% | 96.47% | 100.00% | 96.35% | 92.05% | 97.54% |
| [wiring 0.2.4][wiring] | 95.95% | 50.31% | 100.00% | 96.34% | 92.05% | 97.42% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.06%\**</span> | <span title="validated on-demand with error">*2.19%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 6.65% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*50.00%\**</span> <span title="validated upfront with error">*2.72%\**</span> | <span title="unvalidated">*49.84%\**</span> <span title="validated upfront with error">*49.97%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*99.99%\**</span> <span title="validated upfront with error">*88.67%\**</span> | <span title="unvalidated">*99.97%\**</span> <span title="validated upfront with error">*100.00%\**</span> | <span title="unvalidated">*91.34%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*23.57%\**</span> | <span title="unvalidated">*99.97%\**</span> <span title="validated upfront with error">*99.90%\**</span> | <span title="unvalidated">*100.00%\**</span> |

## `minecraft_savedata`

This data set is composed of Minecraft player saves that contain highly structured data.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Borrow | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*891.54 µs\**</span> <span title="prepend">*772.00 µs\**</span> | 3.0802 ms | 1.5694 ms | 489348 | 281173 | 249360 | 2.3942 ms |
| [bin-proto 0.12.3][bin-proto] | 2.0404 ms | 2.8459 ms | † | 566975 | 239350 | 231475 | 2.2803 ms |
| [bincode 2.0.1][bincode] | 320.01 µs | 1.9189 ms | 793.10 µs | 367413 | 221291 | 206242 | 1.8266 ms |
| [bincode 1.3.3][bincode1] | 609.44 µs | 1.9340 ms | 879.70 µs | 569975 | 240525 | 231884 | 2.2696 ms |
| [bitcode 0.6.6][bitcode] | 105.98 µs | 1.3282 ms | 153.13 µs | 327688 | 200947 | 182040 | 741.13 µs |
| [borsh 1.5.7][borsh] | 571.18 µs | 1.8775 ms | † | 446595 | 234236 | 209834 | 1.9916 ms |
| [capnp 0.23.2][capnp] | 445.10 µs | † | † | 803896 | 335606 | 280744 | 3.3118 ms |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 729.34 µs | 4.5987 ms | 3.3156 ms | 1109831 | 344745 | 274333 | 3.3803 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 3.8889 ms | 11.680 ms | † | 1109821 | 344751 | 274345 | 3.2395 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 1.9529 ms | 4.4651 ms | 3.1120 ms | 1109821 | 344751 | 274345 | 3.2533 ms |
| [columnar 0.11.1][columnar] | 224.17 µs | 1.9873 ms <span title="copy_from">*803.83 µs\**</span> | † | 563728 | 249696 | 217582 | 1.5095 ms |
| [databuf 0.5.0][databuf] | 239.45 µs | 1.8601 ms | 825.76 µs | 356311 | 213062 | 198403 | 1.7681 ms |
| [dlhn 0.1.7][dlhn] | 737.67 µs | 2.7579 ms | † | 366496 | 220600 | 205586 | 1.8086 ms |
| [flatbuffers 25.12.19][flatbuffers] | 3.4004 ms | † | † | 849472 | 347816 | 294871 | 3.2716 ms |
| [flexbuffers 25.2.10][flexbuffers] | 8.1964 ms | 7.3713 ms | 6.2319 ms | 1187688 | 557642 | 553730 | 5.6510 ms |
| json:<br> [flexon 0.4.5][flexon] | 2.6706 ms | 4.5313 ms | † | 1623191 | 466527 | 359157 | 5.5438 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 3.9723 ms | 6.8602 ms | † | 1623191 | 466527 | 359157 | 5.5336 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 2.3349 ms | 4.6719 ms | † | 1623191 | 466527 | 359157 | 5.5571 ms |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 794.28 µs | 3.0344 ms | † | 391251 | 236877 | 220395 | 1.9516 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 1.5730 ms | 3.0985 ms | 1.6651 ms | 424533 | 245214 | 226077 | 2.1766 ms |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 337.42 µs | 2.3655 ms | 998.23 µs | 416025 | 243812 | 224965 | 2.0294 ms |
| [minicbor 1.0.0][minicbor] | 578.65 µs | 3.4813 ms | 1.8737 ms | 428773 | 249857 | 228630 | 2.0554 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 5.3621 ms | 4.0621 ms | 2.8701 ms | 449745 | 252432 | 230965 | 2.1333 ms |
| [nanoserde 0.2.1][nanoserde] | 195.80 µs | 1.9733 ms | † | 567975 | 239930 | 231872 | 2.2939 ms |
| [nibblecode 0.1.0][nibblecode] | 135.58 µs | † | † | 603928 | 376906 | 347808 | 3.1296 ms |
| [postcard 1.1.1][postcard] | 442.54 µs | 2.2260 ms | 843.44 µs | 367489 | 221913 | 207244 | 1.9304 ms |
| [pot 3.0.1][pot] | 2.4179 ms | 6.2382 ms | 5.1892 ms | 599125 | 299158 | 247675 | 2.4836 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*1.3321 ms\**</span> <span title="populate + encode">*3.1785 ms\**</span> | 3.5662 ms | † | 596811 | 305319 | 268737 | 2.7819 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*1.2253 ms\**</span> <span title="populate + encode">*3.3162 ms\**</span> | 3.8923 ms | † | 596811 | 305319 | 268737 | 2.7470 ms |
| [rkyv 0.8.10][rkyv] | 272.71 µs | <span title="unvalidated">*1.6158 ms\**</span> <span title="validated upfront with error">*2.0116 ms\**</span> | † | 603776 | 254776 | 219421 | 2.2040 ms |
| [ron 0.10.1][ron] | 7.9929 ms | 26.341 ms | 24.786 ms | 1465223 | 434935 | 342907 | 5.4482 ms |
| [savefile 0.18.6][savefile] | 159.62 µs | 1.9331 ms | † | 566991 | 239362 | 231478 | 2.3743 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 652.55 µs | 2.2436 ms | † | 356311 | 212976 | 198423 | 1.7629 ms |
| [serde-brief 0.1.1][serde-brief] | 1.2567 ms | 5.4341 ms | 3.5022 ms | 1276014 | 373898 | 293384 | 3.4907 ms |
| [serde_bare 0.5.0][serde_bare] | 822.93 µs | 2.4475 ms | † | 356311 | 213062 | 198403 | 1.7687 ms |
| [speedy 0.8.7][speedy] | 204.91 µs | 1.7535 ms | 566.21 µs | 449595 | 234970 | 210192 | 1.8799 ms |
| [wincode 0.2.4][wincode] | 149.81 µs | 1.7636 ms | 642.84 µs | 566975 | 239350 | 231475 | 2.3430 ms |
| [wiring 0.2.4][wiring] | 143.90 µs | 2.0075 ms | † | 566975 | 247810 | 225086 | 2.3270 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*92.178 ns\**</span> | <span title="validated on-demand with error">*478.16 ns\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 865.53 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.8137 ns\**</span> <span title="validated upfront with error">*2.6286 ms\**</span> | <span title="unvalidated">*1.6526 µs\**</span> <span title="validated upfront with error">*2.6332 ms\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.4063 ns\**</span> <span title="validated upfront with error">*124.64 µs\**</span> | <span title="unvalidated">*176.54 ns\**</span> <span title="validated upfront with error">*126.47 µs\**</span> | <span title="unvalidated">*780.29 ns\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.4064 ns\**</span> <span title="validated upfront with error">*316.39 µs\**</span> | <span title="unvalidated">*176.47 ns\**</span> <span title="validated upfront with error">*282.15 µs\**</span> | <span title="unvalidated">*782.21 ns\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Borrow | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*11.89%\**</span> <span title="prepend">*13.73%\**</span> | 26.10% | 9.76% | 66.96% | 71.47% | 73.00% | 30.96% |
| [bin-proto 0.12.3][bin-proto] | 5.19% | 28.25% | † | 57.80% | 83.96% | 78.64% | 32.50% |
| [bincode 2.0.1][bincode] | 33.12% | 41.89% | 19.31% | 89.19% | 90.81% | 88.27% | 40.57% |
| [bincode 1.3.3][bincode1] | 17.39% | 41.56% | 17.41% | 57.49% | 83.55% | 78.50% | 32.65% |
| [bitcode 0.6.6][bitcode] | 100.00% | 60.52% | 100.00% | 100.00% | 100.00% | 100.00% | 100.00% |
| [borsh 1.5.7][borsh] | 18.55% | 42.81% | † | 73.37% | 85.79% | 86.75% | 37.21% |
| [capnp 0.23.2][capnp] | 23.81% | † | † | 40.76% | 59.88% | 64.84% | 22.38% |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 14.53% | 17.48% | 4.62% | 29.53% | 58.29% | 66.36% | 21.93% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 2.73% | 6.88% | † | 29.53% | 58.29% | 66.35% | 22.88% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 5.43% | 18.00% | 4.92% | 29.53% | 58.29% | 66.35% | 22.78% |
| [columnar 0.11.1][columnar] | 47.28% | 40.45% <span title="copy_from">*100.00%\**</span> | † | 58.13% | 80.48% | 83.67% | 49.10% |
| [databuf 0.5.0][databuf] | 44.26% | 43.21% | 18.54% | 91.97% | 94.31% | 91.75% | 41.92% |
| [dlhn 0.1.7][dlhn] | 14.37% | 29.15% | † | 89.41% | 91.09% | 88.55% | 40.98% |
| [flatbuffers 25.12.19][flatbuffers] | 3.12% | † | † | 38.58% | 57.77% | 61.74% | 22.65% |
| [flexbuffers 25.2.10][flexbuffers] | 1.29% | 10.90% | 2.46% | 27.59% | 36.04% | 32.88% | 13.12% |
| json:<br> [flexon 0.4.5][flexon] | 3.97% | 17.74% | † | 20.19% | 43.07% | 50.69% | 13.37% |
| json:<br> [serde_json 1.0.140][serde_json] | 2.67% | 11.72% | † | 20.19% | 43.07% | 50.69% | 13.39% |
| json:<br> [simd-json 0.15.1][simd-json] | 4.54% | 17.21% | † | 20.19% | 43.07% | 50.69% | 13.34% |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 13.34% | 26.49% | † | 83.75% | 84.83% | 82.60% | 37.98% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 6.74% | 25.94% | 9.20% | 77.19% | 81.95% | 80.52% | 34.05% |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 31.41% | 33.98% | 15.34% | 78.77% | 82.42% | 80.92% | 36.52% |
| [minicbor 1.0.0][minicbor] | 18.32% | 23.09% | 8.17% | 76.42% | 80.42% | 79.62% | 36.06% |
| [nachricht-serde 0.4.0][nachricht-serde] | 1.98% | 19.79% | 5.34% | 72.86% | 79.60% | 78.82% | 34.74% |
| [nanoserde 0.2.1][nanoserde] | 54.13% | 40.74% | † | 57.69% | 83.75% | 78.51% | 32.31% |
| [nibblecode 0.1.0][nibblecode] | 78.17% | † | † | 54.26% | 53.31% | 52.34% | 23.68% |
| [postcard 1.1.1][postcard] | 23.95% | 36.11% | 18.16% | 89.17% | 90.55% | 87.84% | 38.39% |
| [pot 3.0.1][pot] | 4.38% | 12.89% | 2.95% | 54.69% | 67.17% | 73.50% | 29.84% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*7.96%\**</span> <span title="populate + encode">*3.33%\**</span> | 22.54% | † | 54.91% | 65.82% | 67.74% | 26.64% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*8.65%\**</span> <span title="populate + encode">*3.20%\**</span> | 20.65% | † | 54.91% | 65.82% | 67.74% | 26.98% |
| [rkyv 0.8.10][rkyv] | 38.86% | <span title="unvalidated">*49.75%\**</span> <span title="validated upfront with error">*39.96%\**</span> | † | 54.27% | 78.87% | 82.96% | 33.63% |
| [ron 0.10.1][ron] | 1.33% | 3.05% | 0.62% | 22.36% | 46.20% | 53.09% | 13.60% |
| [savefile 0.18.6][savefile] | 66.40% | 41.58% | † | 57.79% | 83.95% | 78.64% | 31.21% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 16.24% | 35.83% | † | 91.97% | 94.35% | 91.74% | 42.04% |
| [serde-brief 0.1.1][serde-brief] | 8.43% | 14.79% | 4.37% | 25.68% | 53.74% | 62.05% | 21.23% |
| [serde_bare 0.5.0][serde_bare] | 12.88% | 32.84% | † | 91.97% | 94.31% | 91.75% | 41.90% |
| [speedy 0.8.7][speedy] | 51.72% | 45.84% | 27.04% | 72.89% | 85.52% | 86.61% | 39.42% |
| [wincode 0.2.4][wincode] | 70.74% | 45.58% | 23.82% | 57.80% | 83.96% | 78.64% | 31.63% |
| [wiring 0.2.4][wiring] | 73.65% | 40.04% | † | 57.80% | 81.09% | 80.88% | 31.85% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.53%\**</span> | <span title="validated on-demand with error">*36.91%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 0.16% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*49.98%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*10.68%\**</span> <span title="validated upfront with error">*0.01%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*99.96%\**</span> <span title="validated upfront with error">*0.14%\**</span> | <span title="unvalidated">*100.00%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*99.99%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.06%\**</span> | <span title="unvalidated">*99.75%\**</span> |

## `mk48`

This data set is composed of mk48.io game updates that contain data with many exploitable patterns and invariants.

### Raw data

For operations, time per iteration; for size, bytes. Lower is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*4.7650 ms\**</span> <span title="prepend">*2.3025 ms\**</span> | 8.3024 ms | 1704643 | 1294259 | 1245668 | 10.644 ms |
| [bin-proto 0.12.3][bin-proto] | 5.6783 ms | 6.4883 ms | 1791489 | 1127998 | 1051146 | 9.2056 ms |
| [bincode 2.0.1][bincode] | 1.0438 ms | 3.9709 ms | 1406257 | 1117802 | 1062438 | 8.5272 ms |
| [bincode 1.3.3][bincode1] | 4.2682 ms | 4.6186 ms | 1854234 | 1141994 | 1048745 | 9.5244 ms |
| [bitcode 0.6.6][bitcode] | 720.85 µs | 2.5251 ms | 971318 | 878034 | 850340 | 2.7774 ms |
| [borsh 1.5.7][borsh] | 3.1371 ms | 2.9382 ms | 1521989 | 1108471 | 1038528 | 8.8321 ms |
| [capnp 0.23.2][capnp] | 2.1681 ms | † | 2724288 | 1546992 | 1239111 | 13.625 ms |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 2.8128 ms | 18.840 ms | 6012539 | 1695215 | 1464951 | 20.869 ms |
| cbor:<br> [ciborium 0.2.2][ciborium] | 25.408 ms | 61.852 ms | 6012373 | 1695146 | 1465025 | 21.484 ms |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 10.440 ms | 18.363 ms | 6012373 | 1695146 | 1465025 | 20.980 ms |
| [columnar 0.11.1][columnar] | 911.50 µs | 3.8987 ms <span title="copy_from">*1.2592 ms\**</span> | 1544752 | 996728 | 897073 | 4.5008 ms |
| [databuf 0.5.0][databuf] | 1.0142 ms | 3.9280 ms | 1319999 | 1062631 | 1008334 | 7.9331 ms |
| [dlhn 0.1.7][dlhn] | 4.8943 ms | 7.5845 ms | 1311281 | 1077520 | 1046095 | 7.6826 ms |
| [flatbuffers 25.12.19][flatbuffers] | 5.1255 ms | † | 2325620 | 1439185 | 1268060 | 12.692 ms |
| [flexbuffers 25.2.10][flexbuffers] | 40.860 ms | 37.440 ms | 5352680 | 2658295 | 2777967 | 32.168 ms |
| json:<br> [flexon 0.4.5][flexon] | 14.251 ms | 22.429 ms | 9390461 | 2391679 | 1842767 | 35.659 ms |
| json:<br> [serde_json 1.0.140][serde_json] | 22.101 ms | 31.578 ms | 9390461 | 2391679 | 1842767 | 35.673 ms |
| json:<br> [simd-json 0.15.1][simd-json] | 13.089 ms | 25.109 ms | 9390461 | 2391679 | 1842767 | 35.451 ms |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 1.7325 ms | 6.5499 ms | 1458773 | 1156055 | 1137788 | 8.6478 ms |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 11.216 ms | 10.881 ms | 1745322 | 1261627 | 1228923 | 10.358 ms |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 1.9828 ms | 5.8860 ms | 1794467 | 1273669 | 1242301 | 10.254 ms |
| [minicbor 1.0.0][minicbor] | 2.4422 ms | 11.316 ms | 1777386 | 1276218 | 1252558 | 11.062 ms |
| [nachricht-serde 0.4.0][nachricht-serde] | 31.827 ms | 16.913 ms | 1770060 | 1277755 | 1263362 | 11.243 ms |
| [nanoserde 0.2.1][nanoserde] | 918.29 µs | 2.8532 ms | 1812404 | 1134820 | 1053109 | 9.4742 ms |
| [nibblecode 0.1.0][nibblecode] | 525.09 µs | † | 2075936 | 1558718 | 1452904 | 12.495 ms |
| [postcard 1.1.1][postcard] | 2.0307 ms | 4.4212 ms | 1311281 | 1083900 | 1041434 | 7.8078 ms |
| [pot 3.0.1][pot] | 14.572 ms | 30.275 ms | 2604812 | 1482233 | 1298928 | 14.879 ms |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*6.0001 ms\**</span> <span title="populate + encode">*9.9998 ms\**</span> | 9.0501 ms | 1859886 | 1338076 | 1295351 | 11.536 ms |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*5.4264 ms\**</span> <span title="populate + encode">*12.902 ms\**</span> | 12.875 ms | 1859886 | 1338076 | 1295351 | 11.337 ms |
| [rkyv 0.8.10][rkyv] | 1.0757 ms | <span title="unvalidated">*2.3726 ms\**</span> <span title="validated upfront with error">*2.8364 ms\**</span> | 2075936 | 1383779 | 1210377 | 11.982 ms |
| [ron 0.10.1][ron] | 41.620 ms | 157.00 ms | 8677703 | 2233642 | 1826180 | 35.244 ms |
| [savefile 0.18.6][savefile] | 723.84 µs | 2.7483 ms | 1791505 | 1128012 | 1051153 | 9.2648 ms |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 3.4356 ms | 3.4561 ms | 1319999 | 1064380 | 1010708 | 7.7489 ms |
| [serde-brief 0.1.1][serde-brief] | 4.7151 ms | 24.678 ms | 6951772 | 1796265 | 1567819 | 23.639 ms |
| [serde_bare 0.5.0][serde_bare] | 5.2033 ms | 5.1550 ms | 1319999 | 1062645 | 1008349 | 7.9030 ms |
| [speedy 0.8.7][speedy] | 727.64 µs | 2.6569 ms | 1584734 | 1119837 | 1037992 | 9.1487 ms |
| [wincode 0.2.4][wincode] | 603.51 µs | 2.5660 ms | 1791489 | 1127998 | 1051146 | 9.2381 ms |
| [wiring 0.2.4][wiring] | 615.60 µs | 2.9483 ms | 1791489 | 1156963 | 1082815 | 9.5344 ms |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*97.544 ns\**</span> | <span title="validated on-demand with error">*810.65 ns\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 58.348 ns | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*2.8126 ns\**</span> <span title="validated upfront with error">*6.6311 ms\**</span> | <span title="unvalidated">*3.2336 µs\**</span> <span title="validated upfront with error">*6.6328 ms\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*1.4062 ns\**</span> <span title="validated upfront with error">*370.41 µs\**</span> | <span title="unvalidated">*380.30 ns\**</span> <span title="validated upfront with error">*372.56 µs\**</span> | <span title="unvalidated">*271.74 ns\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*1.4060 ns\**</span> <span title="validated upfront with error">*447.51 µs\**</span> | <span title="unvalidated">*380.69 ns\**</span> <span title="validated upfront with error">*455.04 µs\**</span> | <span title="unvalidated">*270.46 ns\**</span> |

### Comparison

Relative to best. Higher is better.

#### Serialize / deserialize speed and size

| Crate | Serialize | Deserialize | Size | Zlib | Zstd | Zstd Time |
|---|--:|--:|--:|--:|--:|--:|
| [bilrost 0.1013.0][bilrost] | <span title="encode">*11.02%\**</span> <span title="prepend">*22.81%\**</span> | 15.17% | 56.98% | 67.84% | 68.26% | 26.09% |
| [bin-proto 0.12.3][bin-proto] | 9.25% | 19.41% | 54.22% | 77.84% | 80.90% | 30.17% |
| [bincode 2.0.1][bincode] | 50.31% | 31.71% | 69.07% | 78.55% | 80.04% | 32.57% |
| [bincode 1.3.3][bincode1] | 12.30% | 27.26% | 52.38% | 76.89% | 81.08% | 29.16% |
| [bitcode 0.6.6][bitcode] | 72.84% | 49.87% | 100.00% | 100.00% | 100.00% | 100.00% |
| [borsh 1.5.7][borsh] | 16.74% | 42.86% | 63.82% | 79.21% | 81.88% | 31.45% |
| [capnp 0.23.2][capnp] | 24.22% | † | 35.65% | 56.76% | 68.63% | 20.38% |
| cbor:<br> [cbor4ii 1.0.0][cbor4ii] | 18.67% | 6.68% | 16.15% | 51.79% | 58.05% | 13.31% |
| cbor:<br> [ciborium 0.2.2][ciborium] | 2.07% | 2.04% | 16.16% | 51.80% | 58.04% | 12.93% |
| cbor:<br> [serde_cbor 0.11.2][serde_cbor] | 5.03% | 6.86% | 16.16% | 51.80% | 58.04% | 13.24% |
| [columnar 0.11.1][columnar] | 57.61% | 32.30% <span title="copy_from">*100.00%\**</span> | 62.88% | 88.09% | 94.79% | 61.71% |
| [databuf 0.5.0][databuf] | 51.77% | 32.06% | 73.58% | 82.63% | 84.33% | 35.01% |
| [dlhn 0.1.7][dlhn] | 10.73% | 16.60% | 74.07% | 81.49% | 81.29% | 36.15% |
| [flatbuffers 25.12.19][flatbuffers] | 10.24% | † | 41.77% | 61.01% | 67.06% | 21.88% |
| [flexbuffers 25.2.10][flexbuffers] | 1.29% | 3.36% | 18.15% | 33.03% | 30.61% | 8.63% |
| json:<br> [flexon 0.4.5][flexon] | 3.68% | 5.61% | 10.34% | 36.71% | 46.14% | 7.79% |
| json:<br> [serde_json 1.0.140][serde_json] | 2.38% | 3.99% | 10.34% | 36.71% | 46.14% | 7.79% |
| json:<br> [simd-json 0.15.1][simd-json] | 4.01% | 5.01% | 10.34% | 36.71% | 46.14% | 7.83% |
| messagepack:<br> [msgpacker 0.4.8][msgpacker] | 30.31% | 19.22% | 66.58% | 75.95% | 74.74% | 32.12% |
| messagepack:<br> [rmp-serde 1.3.0][rmp-serde] | 4.68% | 11.57% | 55.65% | 69.60% | 69.19% | 26.81% |
| messagepack:<br> [zerompk 0.3.2][zerompk] | 26.48% | 21.39% | 54.13% | 68.94% | 68.45% | 27.09% |
| [minicbor 1.0.0][minicbor] | 21.50% | 11.13% | 54.65% | 68.80% | 67.89% | 25.11% |
| [nachricht-serde 0.4.0][nachricht-serde] | 1.65% | 7.45% | 54.87% | 68.72% | 67.31% | 24.70% |
| [nanoserde 0.2.1][nanoserde] | 57.18% | 44.13% | 53.59% | 77.37% | 80.75% | 29.32% |
| [nibblecode 0.1.0][nibblecode] | 100.00% | † | 46.79% | 56.33% | 58.53% | 22.23% |
| [postcard 1.1.1][postcard] | 25.86% | 28.48% | 74.07% | 81.01% | 81.65% | 35.57% |
| [pot 3.0.1][pot] | 3.60% | 4.16% | 37.29% | 59.24% | 65.46% | 18.67% |
| protobuf:<br> [prost 0.14.1][prost] | <span title="encode">*8.75%\**</span> <span title="populate + encode">*5.25%\**</span> | 13.91% | 52.22% | 65.62% | 65.65% | 24.08% |
| protobuf:<br> [protobuf 3.7.2][protobuf] | <span title="encode">*9.68%\**</span> <span title="populate + encode">*4.07%\**</span> | 9.78% | 52.22% | 65.62% | 65.65% | 24.50% |
| [rkyv 0.8.10][rkyv] | 48.81% | <span title="unvalidated">*53.07%\**</span> <span title="validated upfront with error">*44.39%\**</span> | 46.79% | 63.45% | 70.25% | 23.18% |
| [ron 0.10.1][ron] | 1.26% | 0.80% | 11.19% | 39.31% | 46.56% | 7.88% |
| [savefile 0.18.6][savefile] | 72.54% | 45.82% | 54.22% | 77.84% | 80.90% | 29.98% |
| scale:<br> [parity-scale-codec 3.7.5][parity-scale-codec] | 15.28% | 36.43% | 73.58% | 82.49% | 84.13% | 35.84% |
| [serde-brief 0.1.1][serde-brief] | 11.14% | 5.10% | 13.97% | 48.88% | 54.24% | 11.75% |
| [serde_bare 0.5.0][serde_bare] | 10.09% | 24.43% | 73.58% | 82.63% | 84.33% | 35.14% |
| [speedy 0.8.7][speedy] | 72.16% | 47.39% | 61.29% | 78.41% | 81.92% | 30.36% |
| [wincode 0.2.4][wincode] | 87.01% | 49.07% | 54.22% | 77.84% | 80.90% | 30.06% |
| [wiring 0.2.4][wiring] | 85.30% | 42.71% | 54.22% | 75.89% | 78.53% | 29.13% |

#### Zero-copy deserialization speed

| Crate | Access | Read | Update |
|---|--:|--:|--:|
| [capnp 0.23.2][capnp] | <span title="validated on-demand with error">*1.44%\**</span> | <span title="validated on-demand with error">*46.91%\**</span> | ‡ |
| [columnar 0.11.1][columnar] | 2.41% | ‡ | ‡ |
| [flatbuffers 25.12.19][flatbuffers] | <span title="unvalidated">*49.99%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*11.76%\**</span> <span title="validated upfront with error">*0.01%\**</span> | ‡ |
| [nibblecode 0.1.0][nibblecode] | <span title="unvalidated">*99.99%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.10%\**</span> | <span title="unvalidated">*99.53%\**</span> |
| [rkyv 0.8.10][rkyv] | <span title="unvalidated">*100.00%\**</span> <span title="validated upfront with error">*0.00%\**</span> | <span title="unvalidated">*99.90%\**</span> <span title="validated upfront with error">*0.08%\**</span> | <span title="unvalidated">*100.00%\**</span> |

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
