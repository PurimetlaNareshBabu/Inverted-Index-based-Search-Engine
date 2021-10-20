# Inverted-Index-based-Search-Engine

# inverted_index

A C++ implementation of Reversed-index search engine.

# Implementation

In each implementation, there are 3 main modules to process: input, preprocessing_document and query function.

- input function: read from product_names.txt into `vector<string> strs`
- preprocessing_document function: from `vector<string> strs`, prepare data struct for quering.
- query function: from data stucture created in preprocessing_document function, query is preformed.

In each algorithm, I used different data structures to perform quering.

## Reversed-index

A [Trie](https://vnoi.info/wiki/algo/data-structures/trie), also called digital tree, radix tree or prefix tree, is a kind of search tree—an ordered tree data structure used to store a dynamic set or associative array where the keys are usually strings.

In each node, there are 2 variables:

```
set<int> v_set; // contain every docid of document which contain keyword
unordered_map<char, Trie*> map; // contain pointers to next node of a Trie tree
```

# How To Run

Inside the code, there are 2 functions:

- custom_test(): custom query input from console
- test_with_100_query(): read query from the file `100_query.txt` and run query into file `100_query_result.txt`

Code default is custom_test()

You can modify the code into test_with_100_query() for runing with 100_query.txt test.

## Reversed-index

```
cd reversed_index/
g++ -std=c++17 main.cpp -o main && ./main product_names.txt
```
# Evaluation

The estimate time of preprocessing_document function is 3-6s.

### Reversed-index

Each query last 1-2s to perform

Result doesn't estimate the relevance of documents to a given search query

