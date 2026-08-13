# BLNS23 q=7933

Standalone extraction of the q=7933 blind-signature research implementation used by `patirckk1994/tradep2p2`.

Target construction: W. Beullens, V. Lyubashevsky, N. K. Nguyen, G. Seiler, *Lattice-Based Blind Signatures: Short, Efficient, and Round-Optimal* (CCS 2023 / IACR ePrint 2023/077).

## Source integrity

The cryptographic implementation under `include/tradep2p/` and `src/` is copied byte-for-byte from `patirckk1994/tradep2p2` branch `agents/backup-branch-for-playground`, source commit:

`cebd9d9fde578678849ded0bc3b4ccf5284f8f33`

It is intentionally **not refactored, renamed, reformatted, optimized, or otherwise edited** during extraction. The existing `tradep2p::blns7933` namespace and file names are preserved so that source blobs can be compared directly with the original repository.

Only standalone packaging/build files in this repository are new.

## C++ library

The C++ substrate uses the paper parameter shape `q = 7933`, `d = 512` and contains the exact/auditable NTRU/Falcon-style trapdoor, Gaussian sampling, LDL/tree sampling, signing and verification path from the source repository.

Dependencies:

- C++20
- Boost headers
- OpenSSL Crypto
- CMake >= 3.20

Build:

```sh
cmake -S . -B build -DCMAKE_BUILD_TYPE=Release
cmake --build build -j
```

The target is:

```text
blns23_q7933
```

with alias:

```text
blns23::q7933
```

By default CMake builds a static library. Set `BUILD_SHARED_LIBS=ON` for a shared library.

## zkVM prover

`blindsig-prover-q7933/` is copied from the same source snapshot without modification. It contains the Rust/RISC Zero proof implementation used for the q=7933 blind-signature protocol and credential-presentation statement.

It remains a separate process/workspace exactly as in the original architecture rather than being rewritten into the C++ library.

## Status

Research / experimental cryptography. This packaging does not turn the implementation into an audited production primitive. Preserve the original review warnings and validate the construction independently before relying on it for real assets.

## License

MIT; see `LICENSE`.
