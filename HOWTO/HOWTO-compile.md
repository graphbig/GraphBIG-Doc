<pre style="display:inline-block;line-height:13px;">
  ________                    .__   __________.___  ________
 /  _____/___________  ______ |  |__\______   \   |/  _____/
/   \  __\_  __ \__  \ \____ \|  |  \|    |  _/   /   \  ___
\    \_\  \  | \// __ \|  |_> >   Y  \    |   \   \    \_\  \
 \______  /__|  (____  /   __/|___|  /______  /___|\______  /
        \/           \/|__|        \/       \/            \/
</pre>

# GraphBIG: How to compile

## Requirements

GraphBIG requires no external libraries. The following compilers are required (tested). 

- CPU benchmarks: gcc/g++ with c++0x support (>4.3)
- GPU benchmarks: CUDA SDK (5.5-7.0 tested)
- Linux OS: Ubuntu/Debian/RHEL tested

The OS dependency is coming from the profiling code. It can be removed by disabling all profiling related components. (defined in common/perf.h)

## Compile

GraphBIG has three benchmark categories:

- benchmark: (default) CPU benchmarks
- csr_bench: CPU benchmarks using CSR data format
- gpu_bench: GPU benchmarks

To compile benchmarks in each category, just get into the corresponding directory and type _"make all"_. To cleanup previous compiling, just use _"make clean"_ in a similar way. For example:

```sh
$ cd benchmark
$ make clean
$ make all
```

To compile only one particular benchmark, just get into the benchmark directory and use _"make all"_. 

Note: GraphBIG incorporates the source code of libpfm, which is a library for performance monitoring. It is used to convert performance counter names in string format to the corresponding hex codes. No extra installation is required. The source code of libpfm is in _tools/_ and will automatically unpacked, compiled, and linked during compiling. The compiling of libpfm will be performed by each category level Makefile. It can also be compile separately by  calling _make all_ in _tools/_. If the category level Makefiles are never called, users should use the Makfile in _tools/_ before compiling separate benchmarks.

## Compile flags

GraphBIG incorporates a set of compile flags to control generated executable files. The details are listed below.

|Name|Parameter|Default|Usage|
|----|---------|-------|-----|
|PFM|PFM=0|1|disable libpfm (generic linux perf events are still supported)|
|DEBUG|DEBUG=1|0|enable debug flag|
|VERIFY|VERIFY=1|0|enable verification mode, nondeterministic outputs are disabled|
|OUTPUT|OUTPUT=1|0|enable detailed graph property output|
|SIM|SIM=1|0|enable annotations for indicating simulation start/end points| 
|OMP|OMP=1|0|(only available for csr_bench) use openmp for parallel threads. otherwise, use pthread instead|
|PERF|PERF=0|1|(only available for csr_bench) disable all profiling related codes|
|Others|||Internal usage only|

Example:

```sh
$ make DEBUG=1 PFM=0 all
```

More details can be found in the _common.mk_ file in each category diretory. 



