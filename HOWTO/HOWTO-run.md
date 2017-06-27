<pre style="display:inline-block;line-height:13px;">
  ________                    .__   __________.___  ________
 /  _____/___________  ______ |  |__\______   \   |/  _____/
/   \  __\_  __ \__  \ \____ \|  |  \|    |  _/   /   \  ___
\    \_\  \  | \// __ \|  |_> >   Y  \    |   \   \    \_\  \
 \______  /__|  (____  /   __/|___|  /______  /___|\______  /
        \/           \/|__|        \/       \/            \/
</pre>

# GraphBIG: How to run

## Test run

It is fairly easy to perform a test run in GraphBIG. Just get into the directory of a particular benchmark and use _"make run"_. The output will be stored in a log file named _output.log_. An example is shown below.

```sh
$ cd benchmark
$ cd bench_BFS
$ make run
$ cat output.log
```

## General

The execution of GraphBIG benchmarks all follow the below format.

```sh
$ ./<exe> --<arg-name> <arg-value> ...
```

Each argument has an argument name and a corresponding value (except for perf arguments). The argument name should be started with two consecutive dashes. Like typical linux applications, the argument value cannot contain space/tab. If space/tab is really needed, it can be wrapped up in a string in commas. Each argument in GraphBIG benchmarks has a default value. If no input is specified, the default value will be used.

## Benchmarks

GraphBIG has three benchmark categories:

- benchmark: (default) CPU benchmarks
- csr_bench: CPU benchmarks using CSR data format
- gpu_bench: GPU benchmarks

The benchmarks with their corresponding directory names are listed below. 

|Benchmark|CPU(benchmark/)|GPU(gpu_bench/)|CPU-CSR(csr_bench)|
|---------|----------|--------|--------|
|BFS|bench_BFS|gpu_BFS|csr_BFS|
|DFS|bench_DFS|||
|Graph Construction|bench_graphConstruct|||
|Graph Update|bench_graphUpdate|||
|Topology Morphing|bench_TopoMorph|||
|Shortest Path|bench_shortestPath|gpu_SSSP|csr_SSSP|
|kCore Decomposition|bench_kCore|gpu_kCore|csr_kCore|
|Connected Component|bench_connectedComp|gpu_ConnectedComp|csr_CComp|
|Graph Coloring||gpu_GraphColoring|csr_GraphColoring|
|Triangle Count|bench_triangleCount|gpu_TriangleCount|csr_TC|
|Gibbs Inference|bench_gibbsInference|||
|Degree Centrality|bench_degreeCentr|gpu_DegreeCentr|csr_DC|
|Betweenness Centrality|bench_betweennessCentr|gpu_BetweennessCentr||

Some GPU benchmarks (such as BFS) have multiple variations:

- topo_thread_centric (ttc): topological-driven & thread-centric
- topo_warp_centric (twc): topological-driven & warp-centric
- data_thread_centric (dtc): data-driven & thread-centric
- data_warp_centric (dwc): data-driven & warp-centric
- topo_atomic (ta): topological-driven & atomic-inst

(For detailed explanation about topological-/data-driven and thread-/warp-centric, please refer to _Nagesh B. Lakshminarayana, "Efficient graph algorithm execution on data-parallel architectures", dissertation, Georgia Tech_)

## Arguments

GraphBIG benchmarks contains three types of arguments, global arguments, local arguments, and perf arguments.

- Global arguments: arguments that are shared among all benchmarks, such as _threadnum_, _dataset_, etc.
- Local arguments: arguments that are specific to particular benchmarks.
- Perf arguments: arguments for hardware performance counter statistics

### Global arguments

|Name|Default Value|Description|
|:----|:-------------|:-----------|
|threadnum|1|number of parallel threads (ignored in some benchmarks)|
|dataset|dataset/small|input dataset path (contains vertex/edge.csv)|
|separator|"\|"|separator for the csv dataset files|
|help|N/A|print help information|

### Local arguments

Several benchmarks have local arguments that are specific to its own. To get information about the local arguments, just utilize the _help_ argument. For example:

```sh
$ cd benchmark/bench_BFS
$ ./bfs --help
```

### Perf arguments

Perf arguments are in the format of _--perf-event \<perf counter name\>..._
For example:

```sh
$ ./bfs --root 31 --threadnum 1 --dataset ../dataset/small --perf-event PERF_COUNT_HW_CPU_CYCLES PERF_COUNT_HW_INSTRUCTIONS
```

More details about perf arguments can be found in HOWTO-perf.md






