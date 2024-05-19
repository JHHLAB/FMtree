FMtree with kISS
===

## Introduction

This project aims to verify the correctness of k-ordered FM-Indexes constructed using the kISS (k-ordered Induced Suffix Sorting) algorithm. The verification process utilizes FMtree, a fast locating algorithm for FM-Indexes, to ensure the accuracy and reliability of the k-ordered FM-Indexes in genomic data processing. For detailed information about the kISS, please refer to [kISS](https://github.com/jhhung/kISS).

kISS is designed to efficiently construct k-ordered FM-Indexes, optimizing pattern matching tasks in genomics. By leveraging induced-sorting-based suffix array construction, kISS improves time and space complexities. FMtree complements this by providing robust verification and pattern locating capabilities.

For detailed information about the FMtree API, please refer to [README-FMtree.md](README-FMtree.md).

## Requirement
- GNU g++ version 11 or later
- [spdlog](https://github.com/gabime/spdlog)
- [oneTBB](https://github.com/oneapi-src/oneTBB)

## Installation Steps
Begin by installing necessary dependencies:
```
sudo apt install g++-11 make libspdlog-dev libtbb-dev
```

```
git clone https://github.com/JHHLAB/FMtree.git
cd FMtree
git submodule update --init lib/kISS

cd FMtree && make && cd -
cd FMtree_with_kiss && make && cd -
```

## Usage Examples
For detailed information about the FMtree API, please refer to [README-FMtree.md](README-FMtree.md).

## Verify k-ordered FM-Index correctness with FMtree using kISS
### preprocess
```
$ ./preprocess/preprocess --index example/drosophia_chr2.fa
```
> [!note]
> You can choose your own fasta file (ex. chm13v2.0.fa). In this example, we use drasophia_chr2.fa.

### make patterns.txt file for search
```
$ ./FMtree/FMtree
# choose 3 make patterns
# text file name: example/drosophia_chr2.fa.not_N
# pattern length: 16 (any positive integer less than 240)
# pattern number: 10000 (any positive integer)
```

### Indexing for FMtree with kISS construction stage boost
```
$ mkdir -p example/kISS && ln -s ../drosophia_chr2.fa.not_N example/kISS/
$ ./FMtree_with_kiss/FMtree
# choose 1 for index
# Input file name: example/kISS/drosophia_chr2.fa.not_N
# sampling distance(D): 4 (you can choose between 1 < D < 9)
```

### Indexing for origin FMtree
```
$ mkdir -p example/origin && ln -s ../drosophia_chr2.fa.not_N example/origin/
$ ./FMtree/FMtree
# choose 1 for index
# Input file name: example/origin/drosophia_chr2.fa.not_N
# sampling distance(D): 4 (you can choose between 1 < D < 9)
```

### Searching with k-ordered FM index
```
$ ./FMtree_with_kiss/FMtree
# choose 2 for search
# index name: example/kISS/drosophia_chr2.fa.not_N
# you can get the number of matched locations and the checksum value for all locations.
```

### Searching with Origin FMtree
```
$ ./FMtree/FMtree
# choose 2 for search
# index name: example/origin/drosophia_chr2.fa.not_N
# you can get the number of matched locations and the checksum value for all locations.
```
