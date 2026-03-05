# Artifacts for "Cool + Cruel = Dual, and New Benchmarks for Sparse LWE"

This repository contains artifacts belonging to [ePrint 2025/1002](https://eprint.iacr.org/2025/1002), which is accepted at EUROCRYPT 2026.

By executing the command `git submodule init && git submodule update --remote`, you obtain the following two artifacts:

1. Code related to the "drop & solve" and "Cruel+Cool":
  - code to run "Drop+Solve" experiments and resulting data,
  - code to run "Cruel+Cool" experiments and resulting data,
  - code to ease generation of the table with our results,
  - code to generate the rounding error plots in the appendices,
  - code to to generate the cruel bits plots in the appendices.
1. Code related to the "guess & verify" attack:
  - code to run "Guess+Verify" experiments and resulting data.

# Dependencies

The drop & solve attack requires a conda environment in which sage and flatter is installed, see `cool_and_cruel/README.md#Dependencies`.
The guess & verify attack requires a computer with a dedicated graphics card that supports CUDA, see `GPUPrimalHybrid/README.md#requirements-and-dependencies`.

**NOTE:** to repeat the large experiments that are listed in Table 2 of the paper, you need a server with multiple CPU cores, and for guess&verify at least 1 GPU. Be aware that when running the script you should not use *all* threads but rather leave a core to OS and other processes, and when the CPU is multithreaded, to halve the number of threads.

# Documentation

On a general note, it is recommended to use a _conda environment_ for both drop&solve and guess&verify.
One could use the same environment for both.

## Drop&Solve and Cruel+Cool

Further documentation is in `cool_and_cruel/README.md`.

## Guess & Verify

Further documentation is in `GPUPrimalHybrid/README.md`.
The experimental results are collected in `./results-guess-verify/`, which are used to construct the "MLWE parameters" part of Table 2.

# Contributors

- Alexander Karenin, Technology Innovation Institute
- Elena Kirshanova, Technology Innovation Institute
- Julian Nowakowski, Ruhr University Bochum
- Eamonn W. Postlethwaite, King's College London
- Ludo N. Pulles, Centrum Wiskunde & Informatica
- Fernando Virdia, University of Surrey
- Paul Vié, Télécom Paris

Note: affiliation at time of submission