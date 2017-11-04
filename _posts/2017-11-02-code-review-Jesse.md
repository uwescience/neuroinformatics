---
layout: post
comments: true
title:  "Code review by Jesse"
date:   2017-11-02
author: Thomas Mohren
---

# Code review of Jesse Resnick
Jesse gave a presentation about his modeling work, mainly focusing on the challenges he is facing in altering and implementing new ideas into legacy code. Simulation runtime is a major holdup, and we discussed possible solutions to speed up the interfacing between Matlab, Python and C-code. [Jesse's code link](https://github.com/jseresnick/Cnerve)

Jesse works on biophysical modeling of extracellular stimulated neurons. The model has a large parameter space (capacitance, resistance for parts of the neuron membrane), and each simulation currently takes in the order of 10 minutes to run. The model is based on legacy code developed by former graduate students in his lab. Jesse is interested in speeding up the simulations and in automatically adjusting the parameters based on results from the simulations.

# Current Workflow

1. Population initialization (Matlab)

2. Expermental configuration (Matlab), set experimental variables and parameters

3. Simulation in Cython /C

4. Analyze results, adjust new simulations depending on results (Matlab)

# Code/Workflow issues
- Automated tuning based on analysis of the output (closing the loop from step 4 to step 1)
- How to implement this while changing as little as possible of the original C-code.
- Speeding up the simulations
- Legacy code and transitioning between compiled and interpreted programming languages

# Suggestions
- (Jesse): Rewrite code in python and use Cython to improve the performance for most expensive part.
- (Pierre): Implement code in pypy for speedup
- (Ariel): turn dictionary into numbers earlier, C cannot do clever things with dictionaries. This might also give rise to the compilation issues.
- (Ariel): Rule of thumb for writing Cython: write as little python-like language as possible (i.e. objects).
- (Ariel): You can also write C-structs in cython.
- Find out how to work the C code into the wrapper.
