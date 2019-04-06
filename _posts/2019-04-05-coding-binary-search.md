---
layout: post
title: Coding, Binary Search [grade 1]
---

# Coding, Binary Search

## grade 1: binary search

There's a saying about binary search, including mistakes on: dead looping, error boundary checking etc, a total 90% error rate will occur during implementation.

Question:
Given a sorted, non-descending array arr, try to find the min i, which makes arr[i] >= n. If there's no existing i, return to -1.

Python version:

```python
def bi_search(arr, n):
    sl = len(arr)
    if sl == 0:
        return -1
    if arr[sl-1] < n:
        return -1
    
    l = 0
    r = sl
    
    while l<r:
        mid = l + (r-l)//2
        if arr[mid] < n:
            l = mid + 1
        else:
            r = mid
    return r

arr = [1, 2, 2, 3, 4, 5, 5, 5, 7]
bi_search(arr, 2)

```

Javascript Version

```javascript
function bi_search(arr, n){
    sl = arr.length;
    if (sl == 0) return -1;
    if (arr[sl-1] < n) return -1;
    var l = 0, r = sl;
    while (l<r){
        mid = l + parseInt((r-l)/2);
        if (arr[mid] < n)
            l = mid + 1;
        else
            r = mid;
    }
    return r;
}
arr = [1, 2, 2, 3, 4, 5, 5, 5, 7];
console.log(bi_search(arr, 2));
```