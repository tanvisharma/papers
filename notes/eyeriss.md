# Eyeriss
## Problem
DNN layer sizes are big and vary in size, making it difficult to efficiently run them on spatial architectures. Particularly, there are various opportunities for leveraging data reuse in DNNs, which comes at the cost of flexibility in hardware. The question is how to design an energy efficient architecture with highest data reuse.

## Idea
![image](https://github.com/tanvisharma/papers/assets/15167916/6a3125d8-051a-44c8-982c-2ba6d8aa8032)
![image](https://github.com/tanvisharma/papers/assets/15167916/0ff6200f-bd7f-41ba-b574-64d5e71dc5ee)

1. Identify the data reuse opportunities including convolutional reuse (sliding window -- both weights and inputs), IFmap reuse (across output channels -- inputs) and Batch reuse (across outputs -- weights). Using these concepts, devised a taxonomy for different types of dataflow -- weight stationary (reduces weight movements), output stationary (reduces partial sum movement) and no local datareuse (reduces dram movement). Introduced their own dataflow -- "Row stationary" which involves data reuse for weights, inputs and partial sums in the horizontal, diagonal and vertical directions in a systolic array architecture.
2. Concept of optimization of compiler or efficient mapping of DNNs to architecture was introduced -- replication and folding were used to map the weights for the case when weight rows are smaller and size of output filter map is smaller than systolic array, respectively.
3. Optimized the energy further using zero-gating or clock gating for computations involving zero weight values and the use of compression to store the sparse weight matrix.

# Evaluation

![image](https://github.com/tanvisharma/papers/assets/15167916/ad910798-3487-4095-8edb-3beeae2a466b)
![image](https://github.com/tanvisharma/papers/assets/15167916/1ac7dd58-f61c-486f-91de-b3470714d8c5)
![image](https://github.com/tanvisharma/papers/assets/15167916/8d20385c-41c8-4eea-9b29-ef9f8a3de9b0)

1. Comparing different dataflows for AlexNet, row stationary achieves the lowest normalized energy/MAC. For conv layers, the energy/MAC from weights in RS is greater than WS and energy/MAC from psums is greater than OS, but overall RS is more efficient by saving on input pixel movements. For FC layers, almost similar trend follows, but NLR also gives similar energy benefits. In terms of storage levels and ALU, FC energy is dominated by DRAM and conv energy is dominated by RF.
2. As expected, with increase in batch size, DRAM access/operation (or opposite of data reuse) reduces.
3. When compared across different PE sizes, WS shows the most significant reduction in energy/op with higher PE size. This implies WS is not that good when weight sizes are larger than array size and performs almost same as OS for larger array size. (why do people use weight stationary then?)
4. RS also gives the best EDP across different batch sizes as compared to other dataflows.
