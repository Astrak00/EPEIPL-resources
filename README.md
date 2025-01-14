# EPEIPL-resources

Resources (ideas) for the EPEIPL project.

## Measuring performance on different architectures

### 1. [Performance measurement on x86]
To measure the performance of a program on x86 architecture, we can use the `perf` tool. 

To use this tool, we can first check the avaiable events by running:
```bash
$ perf list
```

Then, if for example we want to measure the energy consumption of a program, we can use the following command:
```bash
$ perf stat -e power/energy-cores/ -e power/energy-gpu/ -e power/energy-pkg/ -e power/energy-ram/ ./program
```

On my desktop machine, a Ryzen 3800x, the command can only be used with these parameters:
```bash
$ perf stat -e power/energy-pkg/ ./program
```

### 2. [Performance measurement on ARM]
To measure the performance of a program on ARM architecture, we can not use the `perf` tool as it it not avaiable on MacOs for ARM. Thus, to be able to measure the performance of a program on ARM, we have to take a different approach.

We can take a baseline measurement of the energy consumption of the CPU and GPU (either combined or separated). With this information we can establish a baseline of consumption without any other process running but the terminal (no wifi, no bluetooth, nearly reseted, no login items activated...).
We can then measure the energy consumption of the CPU and GPU while running the program and get the difference between the baseline and the program running.
```bash
$ sudo powermetrics 
```

The other option to measure an ARM processor is the total power consumtion of the board, using a RPi for exmaple. We can use a device to check how much power it has consumed during the execution of the program. This is a more accurate way to measure the power consumption of the program, but it is also more expensive and less practical due to the need of an external device and the fact that total board power consumption will be higher than the CPU power consumption.


### 3. [Performance measurement on RISC-V]

To measure this, I have no clue, but the best idea I have is to do the same as the RPi, but with a RISC-V board. I have no idea if there is a tool like `perf` for RISC-V, but I will look for it.


## Measuring performance on different compilers

When using programming languages that have multiple compilers, I will use the most common ones. For example, for C++, I will be using `g++` and `clang++`. For Python, I will be using `cpython` (the default implementation of python basically everyone uses) and `pypy` (a JIT compiler for python). 

### Python
What I will be trying to use in python:
- `cpython` (https://www.python.org/)
- `pypy` (https://pypy.org/)
- `numba` (https://numba.pydata.org/)

### C++
What I will be trying to use in C++:
- `g++` (https://gcc.gnu.org/) 
- `clang++` (https://clang.llvm.org/)

For the optimizations of the compilers, I will be using the following flags:
- `O3` (no optimization)