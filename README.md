# Euclidean Hub Labeling (EHL)

## Introduction

Implementation of Euclidean Hub Labeling (EHL). EHL is an ultrafast optimal path finding algorithm used for finding shortest paths in Euclidean space.
EHL utilises visibility graph and extends hub labeling[1] to build the index used for online pathfinding. The algorithm and details of our implementation of EHL is available in our paper. EHL is licensed under MIT license, which the license is kept anonymous for this submission.


## Dataset

The four benchmarks used by EHL (dao, da2, sc1, and bgmaps) are retrieved from MovingAI (https://movingai.com).
The merged-meshes are provided by the authors of Polyanya [2] and available from repository (https://bitbucket.org/%7B3c286763-d509-45c2-b036-75814ce8955f%7D/)

## Requirements
The following libraries need to be installed in order to reproduce the implementation results.

- CMake: 

For ubuntu users:
```shell script
sudo apt-get install cmake
```

For mac users:
```shell script
brew install cmake
```
- OpenMP: please refer to (https://www.openmp.org) for installation guide

- Google Sparsehash

For ubuntu users:
```shell script
sudo apt-get install sparsehash
```

For mac users:
```shell script
brew install google-sparsehash
```

- Boost geometry - EHL uses boost geometry library to find and check visibility area as required in the algorithm. However, the latest version doesn't handle some precise cases and only version 1.64 is accurate to our precision needs. Boost version 1.64 can be downloaded from here (https://www.boost.org/users/history/version_1_64_0.html)

## Compiling and Running

EHL uses Cmake to compile, certain changes and modifications should be made to CMakeLists.txt based on different machine settings. 

Run "make fast" to compile.

Currently, we provide three bash scripts to quickly reproduce the experimental results reported in our paper.

bash preprocessing_EHL.sh [BENCHMARK_SUITE] 
e.g., run "bash preprocessing_EHL.sh dao" This bash command creates all the indexes (visibility graph, hub label and EHL) needed for EHL for all the maps in the benchmark suite (dao).

bash benchmark_EHL.sh [BENCHMARK_SUITE] 
e.g., run "bash benchmark_EHL.sh dao" This bash command runs queries for EHL for all the maps in the benchmark suite (dao) using the queries taken from MovingAI.

bash clean_index.sh [BENCHMARK_SUITE]
e.g., run "bash clean_index.sh". This bash command deletes and cleans all indexes of EHL directories.

## To AAAI Reviewer
We thank all anonymous reviewers for their time in reviewing our code.
We have included comments in code where we can to explain the implementation. 
In this section we will provide a short description on how to run our code and reproduce our experiment results.

Our main contribution of EHL is in the following files:
- ebhl.h
- ebhl_query_v2.h

In our paper, we have two phases:
1. Offline Preprocessing
- construction of visibility graph is in "build_visibility_graph.cpp"
- construction of hub label is in "construct_hl.cpp"
- implementation and construction of EHL is in "build_grid_based_hub_labelling.cpp"
We have provided a bash file "preprocessing_EHL.sh" as explained in the previous section which can preprocess all of the above for a given benchmark.

2. Online Query Processing
- running EHL query is in "test_EHL.cpp"
We have provided a bash file "benchmark_EHL.sh" which can run all queries given in the scenario file for a given benchmark.

## References
[1]Li, Y.; U, L. H.; Yiu, M. L.; and Kou, N. M. 2017. An Experimental Study on Hub Labeling based Shortest Path Algorithms. Proceedings of the VLDB Endowment, 11(4): 445–457.

[2] M. Cui, D. D. Harabor, A. Grastien, Compromise-free pathfinding on a navigation mesh, in: Proceedings of the Twenty-Sixth International Joint Conference on Articial Intelligence, IJCAI 2017, 2017, pp. 496-502.
