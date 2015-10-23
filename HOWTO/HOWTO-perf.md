<pre style="display:inline-block;line-height:13px;">
  ________                    .__   __________.___  ________
 /  _____/___________  ______ |  |__\______   \   |/  _____/
/   \  __\_  __ \__  \ \____ \|  |  \|    |  _/   /   \  ___
\    \_\  \  | \// __ \|  |_> >   Y  \    |   \   \    \_\  \
 \______  /__|  (____  /   __/|___|  /______  /___|\______  /
        \/           \/|__|        \/       \/            \/
</pre>

# GraphBIG: How to perf

## Introduction

GraphBIG provides an embeded profiling tool to analyze benchmarks with real-machine runs. The incorporated tool profiles benchmarks by collecting hardware performance counter statistics. Users can control the collected perf counters via benchmark arguments. For example:

```sh
$ ./bfs --perf-event PERF_COUNT_HW_CPU_CYCLES PERF_COUNT_HW_INSTRUCTIONS
```

## Perf arguments

The perf arguments are in the following format. 

```sh
./<benchmark> --perf-event <counter1> <counter2> ...
```

The perf result will be included in the output of stdout with the following format.

```sh
```

Multiple hardware performance counters can be specified. Even 30 counters are still fine. However, since the hardware counter resource in processors is limited, GraphBIG will collect the perf statistics via multiple rounds of execution if necessary. By default, each round of execution collected 4 counters. It can be changed by tuning the parameter _DEFAULT_PERF_GRP_SZ_ defined in _common/perf.h_.

## Perf counters

#### Generic performance counters

Hardware events:

* PERF_COUNT_HW_CPU_CYCLES 

	Total cycles. Be wary of what happens during CPU frequency scaling.

* PERF_COUNT_HW_INSTRUCTIONS
	
	Retired instructions. Be careful, these can be affected by various issues, most notably hardware interrupt counts.

* PERF_COUNT_HW_CACHE_REFERENCES
	
	Cache accesses. Usually this indicates Last Level Cache accesses but this may vary depending on your CPU. This may include prefetches and coherency messages; again this depends on the design of your CPU.

* PERF_COUNT_HW_CACHE_MISSES
	
	Cache misses. Usually this indicates Last Level Cache misses; this is intended to be used in conjunction with the 

* PERF_COUNT_HW_CACHE_REFERENCES 
	
	event to calculate cache miss rates.

* PERF_COUNT_HW_BRANCH_INSTRUCTIONS
	
	Retired branch instructions. Prior to Linux 2.6.34, this used the wrong event on AMD processors.

* PERF_COUNT_HW_BRANCH_MISSES
	
	Mispredicted branch instructions.

* PERF_COUNT_HW_BUS_CYCLES

	Bus cycles, which can be different from total cycles.

* PERF_COUNT_HW_STALLED_CYCLES_FRONTEND 
	
	Stalled cycles during issue. (since Linux 3.0)

* PERF_COUNT_HW_STALLED_CYCLES_BACKEND 
	
	Stalled cycles during retirement. (since Linux 3.0)

Software events:

* PERF_COUNT_SW_CPU_CLOCK

	This reports the CPU clock, a high-resolution per-CPU timer.

* PERF_COUNT_SW_TASK_CLOCK
	
	This reports a clock count specific to the task that is running.

* PERF_COUNT_SW_PAGE_FAULTS
	
	This reports the number of page faults.

* PERF_COUNT_SW_CONTEXT_SWITCHES

	This counts context switches. Until Linux 2.6.34, these were all reported as user-space events, after that they are reported as happening in the kernel.

* PERF_COUNT_SW_CPU_MIGRATIONS

	This reports the number of times the process has migrated to a new CPU.

* PERF_COUNT_SW_PAGE_FAULTS_MIN

	This counts the number of minor page faults. These did not require disk I/O to handle.

* PERF_COUNT_SW_PAGE_FAULTS_MAJ

	This counts the number of major page faults. These required disk I/O to handle.

* PERF_COUNT_SW_ALIGNMENT_FAULTS 

	This counts the number of alignment faults. These happen when unaligned memory accesses happen; the kernel can handle these but it reduces performance. This happens only on some architectures (never on x86). (since Linux 2.6.33)

* PERF_COUNT_SW_EMULATION_FAULTS 

	This counts the number of emulation faults. The kernel sometimes traps on unimplemented instructions and emulates them for user space. This can negatively impact performance. (since Linux 2.6.33)


Cache events:

PERF_COUNT_HW_CACHE\_\<type\>\_\<operation\>_\<stat\>

* type: L1D, L1I, LL, DTLB, ITLB, BPU
* operation: READ, WRITE, PREFETCH
* stat: ACCESS, MISS

#### Architecture-specific performance counters

GraphBIG also supports performance counters that are specific to certain architectures. To support a wide range of existing architectures, we incorporate libpfm library for event encoding. libpfm encodes performance counter names to corresponding hex codes. To check the supported performance counters on a target architecture. A lightweight tool can be found in  _tools/libpfm-4.5.0/examples/_. The _check_events_ tool can print out the information of supported counters.

```sh
$ cd tools/libpfm-4.5.0/examples/
$ ./check_events
```
If the _check_events_ tool doesn't exist, check if the tools are not compiled. You can compile tools as follows.

```sh
$ cd tools/
$ make all
```

The supported architectures include:

- For AMD X86:
               
	* AMD64 K7, K8
  	* AMD64 Fam10h (Barcelona, Shanghai, Istanbul)
  	* AMD64 Fam11h (Turion)
  	* AMD64 Fam12h (Llano)
    * AMD64 Fam14h (Bobcat)
    * AMD64 Fam15h (Bulldozer) (core and uncore)

- For Intel X86:
    * Intel P6 (Pentium II, Pentium Pro, Pentium III, Pentium M)
    * Intel Yonah (Core Duo/Core Solo),
    * Intel Core (Merom, Penryn, Dunnington)
    * Intel Atom
    * Intel Nehalem, Westmere
    * Intel Sandy Bridge
    * Intel Ivy Bridge
    * Intel Haswell
    * Intel Silvermont
    * Intel RAPL (energy consumption)
    * Intel Knights Corner
    * Intel architectural perfmon v1, v2, v3

- For ARM:
    * ARMV7 Cortex A8
    * ARMV7 Cortex A9
    * ARMV7 Cortex A15
    * Qualcomm Krait

- For SPARC
    * Ultra I, II
    * Ultra III, IIIi, III+
    * Ultra IV+
    * Niagara I, Niagara II
    
- For IBM
    * Power 4
    * Power 5
    * Power 6
    * Power 7
    * Power 8
    * PPC970
    * System z (s390x)

- For MIPS
    * Mips 74k
    
    