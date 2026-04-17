# Results of Guess & Verify

This directory contains the experimental results of the [Guess & Verify (G&V) attack](https://github.com/ludopulles/GPUPrimalHybrid).
[Table 2 of the ePrint report](https://eprint.iacr.org/2025/1002.pdf#table.caption.160) shows these results in a compressed form, in the bottom half ("MLWE parameters") under "Guess & Verify".

## Reproduce files

To reproduce the file  and `ternary-q26-w11.csv` (and some parts of `ternary-q26-w11-details.txt`), do the following:

1. Run: `cd ../GPUPrimalHybrid`
2. Modify the file `./attack_params.py` such that the python array `atk_params` has as value:
```python
atk_params = [
	type_ternary() | {'n': 1024, 'q':        41223389, 'w': 11},
]
```

3. Activate the conda environment
4. Run (inside the environment): `python attack.py -o ternary-q26-w11.csv -r5 -w4 -v |& tee ternary-q26-w11-details.txt`.
	Note: `-w4` may not be optimal for your machine, so consult the [README](https://github.com/ludopulles/GPUPrimalHybrid/blob/main/README.md#usage).

## Breakdown of .csv files

Each .csv file shows the results of all the runs for one parameter set.
For example, by following [Reproduce files](#reproduce-files), the attack will run on 5 instances.
See the [README](https://github.com/ludopulles/GPUPrimalHybrid/blob/main/README.md#result-handling) for an explanation of each column.

## Breakdown of .txt files
1. The .txt files first contain a header.
	For example: `# Column 4, weight w=11, Yoda, 4 workers`:
	- `Column 4` indicates that the 4th column from the Benchmarking [paper (Table 9)](https://eprint.iacr.org/2024/1229.pdf#table.caption.9) / [website](https://facebookresearch.github.io/LWE-benchmarking/benchmark) was used as parameter set.
	- Weight `w=11` indicates the Hamming weight of the secret was `s`.
	- `Yoda` is the name of the server, see [Table 1 of the ePrint report](https://eprint.iacr.org/2025/1002.pdf#table.caption.153).
	- `4 workers` indicates that `python attack.py -w4` was used.
2. After this header line, the .txt file contains the estimated cost of the G&V attack, according to the lattice-estimator. This is only an estimate of the number of elementary operations.
3. Then, the G&V attack parameters are shown. For example, `Attack parameters: {'beta': 49, 'eta_svp': 2, 'm': 197, 'k': 768, 'h_': 3}` indicates that G&V:
	- uses blocksize 49 in BKZ,
	- uses Babai Nearest Plane (`eta_svp = 2`),
	- uses `m=197` LWE samples,
	- guesses `k=768` positions of the secret `s`, and
	- guesses that the Hamming weight of those `k` secret positions is `h_=3`.

	Note: if the attack parameters are not in the text file, you probably specified the G&V attack parameters explicitly on the command line, as described in the [README](https://github.com/ludopulles/GPUPrimalHybrid/blob/main/README.md#command-line-arguments).
4. Then the file contains the expected number of iterations before we guess correct and recover the secret.
5. Finally, the average wall time is given.

Note: `ternary-q29-w10-details.txt` and `ternary-q29-w9-details.txt` deviate from this format, and contain more detailed logging of stdout & stderr.
