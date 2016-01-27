<pre style="display:inline-block;line-height:13px;">
  ________                    .__   __________.___  ________
 /  _____/___________  ______ |  |__\______   \   |/  _____/
/   \  __\_  __ \__  \ \____ \|  |  \|    |  _/   /   \  ___
\    \_\  \  | \// __ \|  |_> >   Y  \    |   \   \    \_\  \
 \______  /__|  (____  /   __/|___|  /______  /___|\______  /
        \/           \/|__|        \/       \/            \/
</pre>

# GraphBIG: How to import external dataset


## Introduction

GraphBIG provides a set of datasets with various data sources and sizes (refer to [here](https://github.com/graphbig/graphBIG/wiki/GraphBIG-Dataset) for more details). However, it is also possible to use your own datasets if you want. In most cases, it requires only negligible efforts to use most public graph datasets. 

## Requirements

There're two major requirements for the datasets:

- data format: the data format has to be standard [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) file with header. 
- graph representation: in the data files, the graph should be represented in the form of edge list, that is, each line has a pair of vertices, representing an edge. 

When using default configurations, GraphBIG requires a bit more things (but, that can be changed):

- vertex list: vertex list named as "vertex.csv"
- edge list: edge list named as "edge.csv"
- separator: the csv file separator by default is "|"

## Use external dataset

1. rename your edge file as "edge.csv". If you have a vertex file, rename it as "vertex.csv".
2. put the csv files in the same directory and use the path as the parameter for "--dataset" argument. If your dataset doesn't have vertex list, enable the "EDGES=1" compile flag.
3. if your dataset files are not using "|" as separator, specify your separator in the argument "--separator". 
4. make sure that in the edge file, source vertex is in column 0 and destination vertex is in column 1. 
5. GPU workloads need a compact dataset format. GraphBIG provides a tool (csr\_bench/tool\_genCSR) that can generator the required data from standard CSV format. 




