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
    # boundary check
    if sl == 0:
        return -1
    if arr[sl-1] < n:
        return -1

    # initialization
    l = 0
    r = sl

    while l<r: # sector 1
        mid = l + (r-l)//2 # sector 2
        if arr[mid] < n: # sector 3
            l = mid + 1 # sector 4
        else:
            r = mid # sector 5
    return r

arr = [1, 2, 2, 3, 4, 5, 5, 5, 7]
bi_search(arr, 2)

```

Decipher on the implementation:

Firstly, boundary check and if there's no satisfactory number exists in given array, we may stop early.

Now come to the search part, in sector 1:
We loop from left to right of an array, if you remember we usually for things like this:

for (i = 0; i < len; i++)

And here is an intelligible explanation:
[Why numbering should start at zero](https://www.cs.utexas.edu/users/EWD/transcriptions/EWD08xx/EWD831.html)

About the mid-point part, 

mid = l + (r - l)//2

There's an alternative way:

mid = (l + r)//2

This is also work for python, but will put an adverse effect on stack over flow in c and java, because l + r might cross memory boundary when these 2 numbers are big enough.

And why //2 instead of /2 in python, in python 3, / is the operator to floating-point division and // is to integer division.




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

C Version

```c
#include <stdio.h>

#define ARR_LEN(arr) (sizeof(arr) / sizeof(arr[0]))

int bi_search(int arr[], int len, int n){
    if (len == 0) return -1;
    if (arr[len-1] < n) return -1;
    int l = 0;
    int r = len;
    while (l<r){
        int mid = l + (r-l)/2;
        if (arr[mid] < n)
            l = mid + 1;
        else
            r = mid;
    }
    return l;
}

int main() {
    int n, rst;
    int arr[] = {1, 2, 2, 3, 4, 5, 5, 5, 7};
    int len = ARR_LEN(arr);
    printf("\nPlease input a number: ");
    scanf("%d", &n);
    rst = bi_search(arr, len, n);
    printf("Answer is %d\n", rst);
}

```

[post status: almost done]