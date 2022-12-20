# acc-sparse-net
Modelling different accelerator architectures for CNN

This project is a part of the Practical Deep Learning System Performance course at Columbia University under Prof. Parijat Dube

# Project description
The objective of this project is to replicate the simulated implementation of an "SCNN-like" architecture in TimeLoop. Timeloop is a framework for evaluating and exploring the architecture of the design space of deep neural network architectures. It provides ways to describe an instance of a deep learning problem (like CNNs), the architecture of an accelerator, a way to specify what components of the accelerator are mapped onto which parts of the problem space, and optionally other detailed instructions. It generates some outputs which can be used to extract crucial energy estimations and additionally a file which describes the best way to map the problem onto the given architecture.  and confirm performance metrics reported in the SCNN paper. Secondarily, to do a TimeLoop-based comparative study between SCNN and at least one other proposed sparse CNN accelerator. 

# Repository structure
The repository is fairly simply organized. The main folder is called `architecture`, in which there are three subfolders, each for one architecture. 
* eyerissv2_simple: This folder contains an example implementation of the eyerissv2 architecture from the `Accelergy-Project/timeloop-accelergy-exercises` [repository](https://github.com/Accelergy-Project/timeloop-accelergy-exercises). The paper for this accelerator is linked here.
* scnn: This contains some unfinished work on evaluating the SCNN architecture. We attempted to model the multiplier array and accumulator buffers but were not successful in implementing the required components within the time frame of the project. This direction of the project can be extended later. 
* weight_queue_iaram_oaram: This directory contains the main experimental portion of our project, in which we modeled the portions of the SCNN architecture that we could within the time frame of the project; the design in the directory contains a weight queue, an input activation RAM, and an output activation RAM. 

In each of the architectures, we have provided some files of the form `timeloop-mapper.*.(yaml/xml/log/txt)`, which are the result files that got generated when we ran timeloop on the architectures that we implemented. The energy stats can be found in the `timeloop-mapper.stats.txt` file.

# Instructions to run
Our work was done using the tools in the `Accelergy-Project/timeloop-accelergy-exercises` [repository](https://github.com/Accelergy-Project/timeloop-accelergy-exercises). Please follow the instructions there to set up the docker. Once the docker is up, clone this repository. 

# Results
Running the `timeloop-mapper` tool on our weight-queue design (with IARAM and OARAM removed) on varying levels of data sparsity yielded the following energy efficiencies of the optimal dataflow/mapping:
| Data sparsity | Energy efficiency (pJ/Compute) |
|------|--------|
| 0.1: | 8.175  |
| 0.2: | 13.497 |
| 0.3: | 18.819 |
| 0.4: | 24.141 |
| 0.5: | 29.464 |
| 0.6: | 34.786 |
| 0.7: | 40.108 |
| 0.8: | 45.430 |
| 0.9: | 50.753 |
| 1.0: | 56.075 |