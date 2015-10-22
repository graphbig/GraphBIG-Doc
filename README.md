<pre style="display:inline-block;line-height:13px;">
  ________                    .__   __________.___  ________
 /  _____/___________  ______ |  |__\______   \   |/  _____/
/   \  __\_  __ \__  \ \____ \|  |  \|    |  _/   /   \  ___
\    \_\  \  | \// __ \|  |_> >   Y  \    |   \   \    \_\  \
 \______  /__|  (____  /   __/|___|  /______  /___|\______  /
        \/           \/|__|        \/       \/            \/
</pre>

# GraphBIG-Doc

## Overview
GraphBIG is a graph benchmarking effort initiated by Georgia Tech [HPArch](http://comparch.gatech.edu/hparch/index.html) and IBM [System G](http://systemg.research.ibm.com). Please refer to [GraphBIG](https://github.com/graphbig/graphBIG) for source code of GraphBIG benchmarks.

__GraphBIG-Doc__ repositoray contains documents of GraphBIG benchmark suites, including introduction documents, compile/execution arguments, and advanced programming guide.

## Documents
__HOWTO/__ directory:

- HOWTO-compile.md: _how to compile GraphBIG_
- HOWTO-run.md: _how to run GraphBIG benchmarks_
- HOWTO-perf.md: _how to profile GraphBIG with hardware performance counters_
- HOWTO-simulate.md: _how to simulate GraphBIG with detailed timing simulation_

__advanced/__ directory:

- Dataset-import.md: _how to import new datasets into GraphBIG_
- OpenG-programming-guide.md: _programming guide for openG graph framework_



## Basic usage

- CPU benchmarks:

```sh
$ git clone https://github.com/graphbig/graphBIG.git GraphBIG
$ cd GraphBIG
$ cd benchmark
$ make clean all
$ cd [bench dir]
$ make run
$ cat output.log
```

- GPU benchmarks:

```sh
$ git clone https://github.com/graphbig/graphBIG.git GraphBIG
$ cd GraphBIG
$ cd gpu_bench
$ make clean all
$ cd [bench dir]
$ make run
$ cat output.log
```

## GraphBIG Directories
|Directory|Contents|
|---------:|--------|
|benchmark|CPU benchmarks (default)|
|gpu_bench|GPU benchmarks|
|csr_bench|CPU benchmarks using CSR data format|
|common|Supporting library|
|openG|Graph computing framework|
|tools|Profiling tools|
|dataset|Sample dataset|


## Publication
Lifeng Nai, Yinglong Xia, Ilie G. Tanase, Hyesoon Kim, and Ching-Yung Lin. [GraphBIG: Understanding Graph Computing in the Context of Industrial Solutions](http://nailifeng.org/pubs/sc-graphbig.pdf), To appear in _the proccedings of the International Conference for High Performance Computing, Networking, Storage and Analysis(SC), Nov. 2015_

## Tutorial
[The World is Big and Linked: Whole Spectrum Industry Solutions towards Big Graphs](http://cci.drexel.edu/bigdata/bigdata2015/tutorials.html), _IEEE BigData 2015, Oct. 2015_


## Contact us
1. Submit "Issues" on GitHub
2. Email: Lifeng Nai (lnai3 _at_ gatech.edu / nailifeng _at_ gmail.com)

