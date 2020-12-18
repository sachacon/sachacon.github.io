---
layout: archive
title: "Senior Design"
permalink: /seniordesign/
author_profile: true
redirect_from:
  - /resume
---

FPGA-Based Deep Learning Accelerator Using TVM Compiler
======
* Advising Professor: Michael Orshansky
* Teammates: Jeffrey Marshall, Troy Jackson, Sergio Chacon, Elgin Allen, Zach Sisti, Michael Pontikes

The purpose of this short summary is to cover the results found from testing the efficacy of the Tensor Virtual Machine (TVM) compiler stack [1]. The TVM compiler is a Deep Learning (DL) compiler that focuses on flexibility, being capable of taking different frontend frameworks, compiling the DL models, and then deploying the models as low-level programs to different hardware backends. As a part of the TVM stack, the Versatile Tensor Accelerator (VTA) dual-ISA architecture is used to program the Field Programmable Gate Array (FPGA) [2]. The project focused on benchmarking the compiler’s performance in terms of inference times for Convolutional Neural Networks (CNNs). The compiler also leverages tuners and schedulers to further improve performance. 

To test the capabilities of the TVM compiler, we used a top down structure, beginning with the design of a system based on the compiler, then extending that system to an FPGA, adding in the VTA architecture, deciding on a specific Convolutional Neural Network (CNN) to test, and then finally evaluating the tuners and schedulers provided by the compiler. We combined each of these pieces into a full system that we could research to see different performance results based on different characteristics provided by the compiler. We decided to use ResNet-18 and ResNet-50 so we could see performance changes with different sized CNNs. Implementing the necessary steps to connect these components was involved a main Python control script, a custom VTA bitstream, and a utilization of Remote Procedure Call (RPC) servers. Since the TVM website used the Xilinx PYNQ board in its examples and tutorials, we selected this as the FPGA for our implementation. Our main point of testing involved comparing the inference times of ResNet employing the PYNQ Board's Dual-Core A9-Cortex Processors versus the full FPGA implementation with its Artix-7 family programmable logic. 

We evaluated the performance of each layer of our system and found that the use of an FPGA programmed with the VTA architecture greatly improves inference time, while using a SoC CPU on its own is significantly slower. In the case of ResNet-18, VTA is 2x better than the SoC CPU, while ResNet-50 sees a 5x improvement. We also found that the different autotuner configurations did not significantly improve inference time when compared to the default tuned configuration. After testing the tuners we created our own custom bitstreams, only to find that different clock speeds did not lead to any significant change in performance. Additionally, after examining the resource allocation within the PYNQ board, we discovered that we had an exceedingly high Look-up Table (LUT) usage and an exceedingly low Block Random Access Memory (BRAM) usage.

![SeniorDesignChartComparison](https://github.com/sachacon/sachacon.github.io/blob/master/images/senior_design_chart.png)

For further research, we would recommend teams look into the VTA architecture itself, as it has major memory bottlenecks that could be improved upon by leveraging the BRAM in the FPGA and reducing the high LUT utilization. The autotuner for TVM, AutoTVM, could also be researched further to see how performance changes with different CNNs. Overall, our results showed that leveraging an FPGA for inference applications leads to great performance increases, despite VTA’s suboptimal resource usage. Consequently, the architecture should be improved or recreated in a better form. 

References
------
[1]	T. Chen et al., "TVM: An Automated End-to-End Optimizing Compiler for Deep 
Learning,”  USENIX Assoc., Carlsbad, CA, Rep. 2018.

[2]	T .Moreau et al., “A Hardware-Software Blueprint for Flexible Deep Learning 
Specialization,” Dept. Comp. Science & Eng, Univ. Washington, Seattle, WA, Rep. 
arXiv:1807.04188, 2019.

