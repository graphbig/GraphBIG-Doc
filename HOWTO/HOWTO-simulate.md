<pre style="display:inline-block;line-height:13px;">
  ________                    .__   __________.___  ________
 /  _____/___________  ______ |  |__\______   \   |/  _____/
/   \  __\_  __ \__  \ \____ \|  |  \|    |  _/   /   \  ___
\    \_\  \  | \// __ \|  |_> >   Y  \    |   \   \    \_\  \
 \______  /__|  (____  /   __/|___|  /______  /___|\______  /
        \/           \/|__|        \/       \/            \/
</pre>

# GraphBIG: How to simulate

## Introduction

It is a common practice for architecture research to perform timing/functional simulations with benchmark workloads. To help architecture research, GraphBIG provides support for architectural simulations of both CPU and GPU GraphBIG workloads.

## Hints

Before simulating the workloads directly, there are a few issues should be carefully considered. 

### Benchmark arguments

The default execution argument can be found in each benchmark's Makefile. Detailed explainaion of the benchmark arguments can be found [here](HOWTO-run.md). Please note that it is desirable to use a smaller dataset because of the limitation of regular architecture simulators.

### Section of interest

Each GraphBIG has a data-loading phase, in which the graph data is loaded from files and represented in an in-mem data structure. The data-loading phase usually is fairly long because of the intense disk IO operations. Thus, the simulation should skip the loading phase and focus only on the _section of interest_ (when the graph is actually being processed). To help users get a more accurate starting point of simulations, GraphBIG includes simulation flags to indicate the _section of interest_. The flags are two dummy function calls:

- SIM\_BEGIN: starting point of _section of interest_.

- SIM\_END: ending point of _section of interest_.

To enable the flags, include "SIM=1" at compiling time (further details can be found [here](HOWTO-compile.md)). Users can trigger the timing simulation (or trace generation for trace-driven simulators) when the function call named as "SIM\_BEGIN" is catched. 



