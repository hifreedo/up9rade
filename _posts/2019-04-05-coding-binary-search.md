---
layout: post
title: Coding, Binary Search [grade 1]
---

# Coding, Binary Search

## grade 1: binary search

There's a saying about binary search, including mistakes on: dead looping, error boundary checking etc, a total 90% error rate will occur during implementation.

Question:
Given a sorted, non-descending array arr, try to find the min i, which makes arr[i] >= n. If there's no existing i, return to -1.


```python
def bi_search(s, n):
    sl = len(s)
    if sl == 0:
        return -1
    if s[sl-1] < n:
        return -1
    
    l = 0
    r = sl
    
    while l<r:
        mid = l + (r-l)//2
        if s[mid] < n:
            l = mid + 1
        else:
            r = mid
    return r

s = [1, 2, 2, 3, 4, 5, 5, 5, 7]
bi_search(s, 2)

```