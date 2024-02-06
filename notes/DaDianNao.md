# DaDianNao

Link: https://www.eecg.toronto.edu/~moshovos/000/lib/exe/fetch.php?media=wiki:aca2017:dadiannao.pdf  
Link to DianNao paper: https://users.cs.duke.edu/~lkw34/papers/diannao-asplos2014.pdf  
## Problem
Model sizes increasing exponentially (GBs of data), memory bandwidth is the key bottleneck, especially in fully connected networks.

## Idea
![image](https://github.com/tanvisharma/papers/assets/10654294/72b6b925-bfaa-4638-834e-d8232581d3e9)
1. To eliminate memory accesses, multi-chip architecture to store models on chip (Single chip cannot store the entire model) with DianNao PE (pipelined). To further boost density, eDRAM technology to store all NN datastructures since it ~2.85x higher density compared to SRAM.
2. Hierarchically spatial, where each node (chip) consists of multiple tiles connected via a fat-tree interconnect, and each tile consists of NFUs with banked eDRAM storage to accomodate high internal bandwidth (reading from eDRAM is generally slow). In their design, each node consists of 2 eDRAM banks to store input/output/partial sums and each tile consists of 4 eDRAM banks to store weights
3. Weight stationary dataflow, while activations move around. Each layer is executed in parallel across different nodes/tiles.
4. Supports 32-bit fixed point computations, since it is useful for training.
# Evaluation

![image](https://github.com/tanvisharma/papers/assets/10654294/6c2c3270-2aa7-429c-9c35-8ac353de3d28)


