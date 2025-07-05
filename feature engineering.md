
- Feature hashing
hashing trick converts text data, or categorical attributes with many
values, into a feature vector of arbitrary dimensionality. One-hot encoding and bag-of-words
have a drawback: many unique values will create high-dimensional feature vectors. For
example, if there are one million unique tokens in a collection of text documents, bag-of-words
will produce feature vectors that each have a dimensionality of one million. Working with
such high-dimensional data might be very computationally expensive.

To keep your data manageable, you can use the hashing trick that works as follows. First you
decide on the desired dimensionality of your feature vectors. Then, using a
hash function
,
you first convert all values of your categorical attribute (or all tokens in your collection of
documents) into a number, and then you convert this number into an index of your feature
vector. The process is illustrated in Figure 9.
Let’s illustrate how it would work for converting a text “Love is a doing word” into a feature
vector. Let us have a hash function
h
that takes a string as input and outputs a non-negative
integer, and let the desired dimensionality be
5
. By applying the hash function to each word
and applying the modulo of
5
to obtain the index of the word, we get:
h(love) mod 5= 0
h(is) mod 5= 3
h(a) mod 5= 1
h(doing) mod 5= 3
h(word) mod 5= 4

Then we build the feature vector as,
[1,1,0,2,1]

Indeed, h(love) mod 5= 0, means that we have one word in dimension 0 of the feature vector;
h(is) mod 5= 3 and h(doing) mod 5 = 3 means that we have two words in dimension 3 of the feature vector, and so on. As you can see, there is acollision between words “is” and
“doing”: they both are represented by dimension 3 
The lower the desired dimensionality, the higher are the chances of collision. This is the trade-off between speed and quality of learning.
Commonly used hash functions are
MurmurHash3
,
Jenkins
,
CityHash
, and
MD5
.
4.2.5 Topic Modeling
Topic modeling is a family of techniques that uses unlabeled data, typically in the form of
natural language text documents. The model learns to represent a document as a vector of
topics. For example, in a collection of news articles, the five major topics could be “sports,”
“politics,” “entertainment,” “finance,” and “technology”. Then, each document could be
represented as a five-dimensional feature vector, one dimension per topic:
[0
.
04
,
0
.
5
,
0
.
1
,
0
.
3
,
0
.
06]
The above feature vector represents a document that mixes two major topics: politics (with a
weight of
0
.
5
) and finance (with a weight of
0
.
3
). Topic modeling algorithms, such as
Laten
