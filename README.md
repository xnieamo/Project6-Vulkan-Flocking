Vulkan Flocking: compute and shading in one pipeline!
======================

**University of Pennsylvania, CIS 565: GPU Programming and Architecture, Project 6**

* Xiaomao Ding
* Tested on: Windows 8.1, i7-4700MQ @ 2.40GHz 8.00GB, GT 750M 2047MB (Personal Computer)

### Introduction
This project implements a 2D version of the [Reynolds Boid Algorithm](http://www.red3d.com/cwr/boids/). This algorithm simulates flocks of birds or schools of fish moving in groups. The primary purpose of this project is to explore the Vulkan pipeline and see its differences from OpenGL. This code only implements a naive version of this algorithm. The project in [this repository](https://github.com/xnieamo/Project1-CUDA-Flocking) implements a 3D version of the algorithm in CUDA and provides a series of performance analysis as well.

<p align="center">
  <img src="https://github.com/xnieamo/Project6-Vulkan-Flocking/blob/master/img/Boids.gif?raw=true">
</p>

### Questions
- Why do you think Vulkan expects explicit descriptors for things like generating pipelines and commands?
Vulkan puts data describing the pipelines and commands in GPU memory. Explicit descriptors allows the GPU to optimize memory usage for the commands during program execution.

- Describe a situation besides flip-flop buffers in which you may need multiple descriptor sets to fit one descriptor layout.
If we had a scene with many different textures, we might use multiple descriptors that each read from various textures.

- What are some problems to keep in mind when using multiple Vulkan queues?
Since the different queues can be backed by different hardware, we cannot guarantee that the assigned tasks in the different queues will finish at the same time. Therefore, to avoid the need of synchronization, the queues should be data independent. Additionally, the same buffer could also be used across different queues. This may lead to race conditions if two queues are writing to the buffer at the same time, or one queue may not have finished the calculations that another queue needs for its calculations.

- What is one advantage of using compute commands that can share data with a rendering pipeline?
Because compute commands can run in parallel with the graphics pipeline, sharing data allows calculations to be performed simultaneously while rendering instead of sequentially. This should provide a performance boost.

### Credits

* [Vulkan examples and demos](https://github.com/SaschaWillems/Vulkan) by [@SaschaWillems](https://github.com/SaschaWillems)
