# Inverted-Index-based-Search-Engine
An inverted index for a set of webpages
Suppose we are given a set of webpages W. For our purposes, each webpage
w ∈ W will be considered to be a sequence of words w1, w2, . . . wk. Another
way of representing the webpage could be to maintain a list of words along
with the position(s) of the words in the webpage. For example consider a
web page with the following text:
Data structures is the study of structures for storing data.
This can be represented as
{(data : 1, 10),(structures : 2, 7),(study : 5),(storing : 9)}.
Note that the small connector words like “is”, “the”, “of”, “for” have not
been stored. Words like this are referred to as stop words and are generally
removed since they are very frequent and normally contain no information
about the content of the webpage.
This representation of the webpage is similar to the index we see at the
back of many books which tell us the page numbers where certain important
terms used in the book may be found. In fact, we can refer to this as an
1
index for the webpage. In mathematical notation we would say that given a
webpage w = w1, w2, . . . , wk, the index of w is
{(u : i1(u), . . . i`(u)) : wij (u) = u, 1 ≤ j ≤ `}.
An index is used to find the location of a particular string (word) in a
specific document or webpage, but when we move to a collection of webpages,
we need to first figure out which of the web pages contain the string. For this
we store an inverted index. Let us try to define an inverted index formally.
Let us suppose we are given a collection C of webpages. For each page
p ∈ C, let us denote by W(p) the set of all words (excluding stop words)
that occur in p. Note that
W(C) = [
p∈C
W(p),
is the set of all words in our collection.
An inverted index for C will contain an entry for each word w ∈ W(C).
This entry will contain tuples of the form (p, k) to indicate that w occurs in
the kth position of page p ∈ C. Using the notation that p[k] denotes the kth
word of page p, we can say that the inverted index of C is defined as
Inv(C) = {(w : {(p, k) : p ∈ C, p[k] = w}) : w ∈ W(C)} .
For example, consider the following (small) collection of documents.
1: Data structures is the study of structures for storing data.
2: Structural engineers collect data about structures
The inverted index for this would be
{(data : {(1,1), (1,10), (2,4)}),
(structures: {(1,2), (1,7), (2,6)}),
(study : {(1,5)}),
(storing : {(1,9)}),
(structural : {(2,1)}),
(engineers : {(2,2)}),
(collect : {(2,3)}) }
2
The web search problem
The web search problem is defined as follows:
Given a collection of webpages C and a sequence of words q1 . . . qk,
find the “most relevant” set of pages p1, p2, . . . p` that contain
as many of q1 . . . qk as possible and return them in the order of
decreasing “relevance.”
The question of how to measure the relevance of a webpage to a particular
query is an involved question with no easy answers. However, for the purpose
of this assignment we will work with a simple scoring function.
A scoring function for search term relevance
One of the simplest scoring function is term frequency-inverse document
frequency. It is used to measure how important a word w is to a webpage
p. It is a product of two factors i.e. term frequency and inverse document
frequency. Given a word w and a webpage p, the relevance score is defined
as
relevancew(p) = tf w(p) ∗ idf w(p)
Term Frequency: It is the total number of occurrence of a word w in a
webpage p, denoted by fw(p). It is normalized by the total number of words
in webpage p, denoted by |W(p)|. It is defined as
tfw(p) = fw(p)
|W(p)|
Inverse document frequency: It is the logarithm of the total number of webpages, denoted by N divide by the logarithm of the number of webpages
nw(p) that contain the word w. It is defined as
idfw(p) = log N
nw(p)
So, if we are given a search query that has a single term, say w, to
return the webpages in order of relevance we have to first extract the entry
corresponding to w from Inv(C) and then calculate the relevance of each page
and return the pages in decreasing order of relevance.
3
Compound searches
In this assignment we will answer three kinds of search queries: AND queries,
OR queries and phrase queries. We now describe these three along with their
scoring methodology.
• OR queries: Given a search query q1 . . . qk, any page that contains any
of the words q1 to qk is a valid answer. The relevance score of a page p
is computed as
relevanceq1...qk
(p) = X
k
i=1
relevanceqi
(p),
and pages are returned in decreasing order of relevance. Note that if
some qi does not occur in page p the relevanceqi
(p) = 0.
• AND queries: Given a search query q1 . . . qk, any page that contains
all of the words q1 to qk is a valid answer. The relevance score of a page
p is computed as
relevanceq1...qk
(p) = X
k
i=1
relevanceqi
(p),
and pages are returned in decreasing order of relevance.
• Phrase queries : Given a search query q1 . . . qk, any page that contains
q1 in position `, q2 in position `+1 and so on till qk in position `+k−1
is said to contain the phrase q1 . . . qk at the position `. Suppose in a
webpage p having |W(p)| words, the phrase q1 . . . qk occurs m times
then the relevance score of page p for this phrase is
relevanceq1...qk
(p) = tfq1...qk
(p) ∗ idfq1...qk
(p)
=
m
|W(p)| − (k − 1) ∗ m
∗ log N
nw(p)
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

# Evaluation

The estimate time of preprocessing_document function is 3-6s.

### Reversed-index

Each query last 1-2s to perform

Result doesn't estimate the relevance of documents to a given search query

