-------------------------------------------------------
# Scalable single-machine PageRank on 70M edge graph
-------------------------------------------------------
This python code was completed as part of an assignment for my Data and Visual Analytics course at The Georgia Insitute of Technology. 

### Introduction
PageRank, named after Google co-founder Larry Page, is an algorithm that measures webpage importance. According to Google: 
>PageRank works by counting the number and quality of links to a page to determine a rough estimate of how important the website is. The underlying assumption is that more important websites are likely to receive more links from other websites
                                                               
The PageRank algorithm implemented in the pagerank.py code file can scale to graph datasets with as many as billions of edges and was implemented using my computer's virtual memory.
>The main idea is to place the dataset in your computer’s (unlimited) virtual memory, as it is often too big to fit in the RAM. When running algorithms on the dataset (e.g., PageRank), 
the operating system will automatically decide when to load the necessary data (subset of whole dataset) into RAM.

See [here]("http://poloclub.gatech.edu/mmap/") for more details on research on virtual memory mapping. The mapping for this algorithm is done using Python's [mmap]("https://docs.python.org/3/library/mmap.html) and [struct]("https://docs.python.org/2/library/struct.html") modules, and PyPy was used to expedite the packing and unpacking functionality of Python.
The PageRank algorithm was used on the [LiveJournal]("https://snap.stanford.edu/data/soc-LiveJournal1.html") graph, which contains almost 70 million edges.
The algorithm outputs the 10 nodes with the highest PageRank scores to a CSV file. 

### Prerequisites
This code requires ##Python 3.6** or later and uses PyPy, which is a Just-In-Time compilation runtime for Python, which supports fast packing and unpacking. You will also need to download the q1_utils.py code to the desired work folder. To install PyPy:

|OS |Instruction      |
|:----------|:-------------|
|Ubuntu |sudo apt-get install pypy|
|MacOS |Install [Homebrew](https://brew.sh/), then run brew install pypy3.|
|Windows |[Download](http://pypy.org/download.html#python2-7-compatible-pypy-5-4-1 ) the package and then install it. |

In the command line, run the following code from the q1_utils folder to learn more about the helper utility that was provided for this assignment.

```pypy q1_utils.py --help```
This code was specifically designed for use on the LieJournal graph dataset, which is an edge list file that can be obtained from the SNAP website here: [download](https://snap.stanford.edu/data/soc-LiveJournal1.html). The q1_utils.py and LiveJournal dataset files must be in the same directory/folder.

### Run
To run the pagerank.py algorithm, follow the steps below. 
1. Since memory mapping works with binary files, the graph’s edge list needs to be converted into its binary format by running the following command at the terminal/command prompt (you only need to do this once):

    ```python q1_utils.py convert <path-to-edgelist.txt>```

    This generates 3 files:
    * A .bin binary file containing edges (source, target) in big-endian “int” C type
    * A .idx: binary file containing (node, degree) in little-endian “int” C type
    * A .json: metadata about the conversion process (required to run pagerank)

2. To execute the PageRank algorithm, type the following code into the command line/terminal:

    ```pypy q1_utils.py pagerank <path to JSON file for LiveJournal>```

    This will output the 10 nodes witht he highest PageRank scores. The default number of iterations is 10. The number of iterations can be updated by adding the desired number to the end of the command:
    ```pypy q1_utils.py pagerank toy-graph/toy-graph.json --iterations 25``
    A file in the format pagerank_nodes_n.txt  for “n” number of iterations will be created.
