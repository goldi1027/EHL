# Euclidean Hub Labeling (EHL)

## Introduction

Implementation of Euclidean Hub Labeling (EHL). EHL is an ultrafast optimal path finding algorithm used for finding shortest paths in Euclidean space.
EHL utilises visibility graph and extends hub labeling[1] to build the index used for online pathfinding. The algorithm and details of our implementation of EHL is available in our paper. EHL is licensed under MIT license, which the license is kept anonymous for this submission.


## Dataset

The four benchmarks used by EHL (dao, da2, sc1, and bgmaps) are retrieved from MovingAI (https://movingai.com).
The merged-meshes are provided by the authors of Polyanya [2] and available from repository (https://bitbucket.org/%7B3c286763-d509-45c2-b036-75814ce8955f%7D/)
We have also provided the scenarios used for testing and experiments in the dataset to reproduce our results.
## Requirements
The following libraries need to be installed in order to reproduce the implementation results.
For installation of the libraries, please follow the guidelines provided by the links.

- CMake: https://cmake.org
- OpenMP: https://www.openmp.org
- Google Sparsehash: https://github.com/justinsb/google-sparsehash
- Boost geometry - EHL uses boost geometry library to find and check visibility area as required in the algorithm. However, the latest version doesn't handle some precise cases and only version 1.64 is accurate to our precision needs. Boost version 1.64 can be downloaded from here (https://www.boost.org/users/history/version_1_64_0.html)

After installing the libraries, as EHL uses Cmake to compile, certain changes and modifications should be made to CMakeLists.txt based on different machine settings.

Then with the Makefile which we have provided, the code could be compiled using "make fast".

## Running

Currently, we provide three bash scripts to quickly reproduce the experimental results reported in our paper.

bash preprocessing_EHL.sh [BENCHMARK_SUITE] 
e.g., run "bash preprocessing_EHL.sh dao" This bash command creates all the indexes (visibility graph, hub label and EHL) needed for EHL for all the maps in the benchmark suite (dao).

bash benchmark_EHL.sh [BENCHMARK_SUITE] 
e.g., run "bash benchmark_EHL.sh dao" This bash command runs queries for EHL for all the maps in the benchmark suite (dao) using the queries taken from MovingAI. The output shows the average runtime of an entire map's queries to the console. 

bash clean_index.sh [BENCHMARK_SUITE]
e.g., run "bash clean_index.sh". This bash command deletes and cleans all indexes of EHL directories.

## Contact
Any questions regarding EHL please contact jinchun.du@monash.edu

## References
[1] Ye Li, Leong Hou U, Man Lung Yiu, Ngai Meng Kou: An Experimental Study on Hub Labeling based Shortest Path Algorithms. Proc. VLDB Endow. 11(4): 445-457 (2017)

[2] Michael Cui, Daniel Damir Harabor, Alban Grastien: Compromise-free Pathfinding on a Navigation Mesh. IJCAI 2017: 496-502
