---
layout: post
title: What is image file [grade 2]
---

# What is image file: Huffman Coding

## grade 2: huffman coding

In previous post, the introduction about [JPEG]({{site.url}}/2018/08/26/what-is-image-jpeg-heif-grade-1.html), we introduced the compression algorithm "Huffman Coding", this post is about it.

Huffman coding is widely used in:

* File compression: zip / gzip
* Image compression: jpeg / png
* Text compression: word2vec
  
A slight note about word2vec, which treats words in corpus as leaf nodes, based on words' frequency as weights, to build corresponding huffman tree.

Now as you could see, we need to understand huffman coding because it was adopted in NLP and CV domains.

There was said huffman coding was invented by David A. Huffman in 1952 while he was attending exam in MIT.

The description in detail [wiki](https://en.wikipedia.org/wiki/Huffman_coding).

Key points:

* Lossless data compression.
* Optimal prefix code.
* Variable length code for different symbols.
* Greedy approach upon frequency of characters.
* Complexity of nlogn to #n unique characters.
* Length of code of character is inverse to its frequency.

Pesudo codes:

```python
 begin
   count frequency of each character
   sort into ascend sequence
   make each char a leaf node (character, frequency, left_son, right_son)
   put nodes into queue Q
   while (Q >= 2) do
     begin
       pop the first/smallest two nodes (n1, n2)
       create a new node with sum of chosen nodes 
       insert new node into sorted Q
     end
   append 0 to left_son and 1 to right_son from the root
   make output for each input character
end
```

Implementation:

```python
# Huffman Coding

class Node():
    def __init__(self,name=None,value=None):
        self._name = name
        self._value = value
        self._left = None
        self._right = None

class HuffmanTree():
    # based on leaf node, grow the tree
    def __init__(self,char_weights):
        # create node for each char
        self.a = [Node(part[0], part[1]) for part in char_weights]
        
        while len(self.a) != 1:
            self.a.sort(key = lambda node : node._value,reverse = True)
            c = Node( value = (self.a[-1]._value + self.a[-2]._value))
            c._left = self.a.pop(-1)
            c._right = self.a.pop(-1)
            self.a.append(c)
        self.root=self.a[0]
        # save huffman code into b, range 10 is the tree depth
        self.b = list(range(10))

    # create code recursively
    def pre(self,tree,length):
        node = tree
        if (not node):
            return
        elif node._name:
            print(node._name + ' : ', end='')
            for i in range(length):
                print(self.b[i], end='')
            print('\n')
            return
        self.b[length] = 0
        self.pre(node._left, length+1)
        self.b[length] = 1
        self.pre(node._right,length+1)
        
    # create huffman code   
    def get_code(self):
        self.pre(self.root, 0)

if __name__ == '__main__':
    # take inputs of char & frequency
    char_weights = [('i',3), ('p',7), ('h',6), ('o',5), ('n',1), ('e',2)]
    tree = HuffmanTree(char_weights)
    tree.get_code()
```

Let's consider another scenario, which explains the usage of Huffman coding well. Assume we have scores of a great amount of students' exams, which range from 0 to 100, and we want to level them from A to E.

One common approach is the if / else if / else statement, something like:
``` python
if score < 61
else if score < 71
else if score < 81
else if score < 91
else:
```

In a first looking, this approach would work, but if take the score distribution into consideration, i.e. majority of the scores are in between 70 ~ 80, we will know this approach is not efficient.

This is the place where Huffman coding works, if we know the distribution as following:

score | A | B | C | D | E
--- | --- | --- | --- | --- | ---
| 91 ~ 100 | 81 ~ 90 | 71 ~ 80 | 61 ~ 70 | 0 ~ 60
| 10% | 20% | 40% | 16% | 14%

How would we rewrite the conditional statement?

```python
if score >=71 and score <81:
else if score >=81 and score < 91:
else if score score >=61 and score < 71:
else if score if score <61:
else:
```

How to deal with "abcc" & how to Huffman decoding.

[post status: half done]