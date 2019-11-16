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
This code requires ##Python 3.X** and requires a TMDb API code to be input to run. To get a TMDb account and API Code:
1. Get a [TMDb account](https://www.themoviedb.org/account/signup)
2. Request an [API key](https://docs.google.com/document/d/e/2PACX-1vQkWjHiLS1Xu2HZNQ7Egv08l_DdPnugoxUOZ0ugqBNHWY529xWB417QoSS0MbIih6PS9gu1Y1D-NFDT/pub)
3. Follow TMDb API [Documentation](https://developers.themoviedb.org/3/getting-started/introduction)

### Run
In the terminal or command window, navigate to the folder where the script is located, and input the following command, substituting your API key:
```python3 script.py <API_KEY>```
This will run the 'script.py' file and execute the code, generating the two aforementioned CSV files. 
