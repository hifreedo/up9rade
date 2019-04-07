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
    arr_len = len(arr)
    # boundary check
    if arr_len == 0:
        return -1
    if arr[arr_len-1] < n:
        return -1

    # initialization
    first = 0
    last = sl

    while first<last: # sector 1
        mid = first + (last-first)//2 # sector 2
        if arr[mid] < n: # sector 3
            first = mid + 1 # sector 4
        else:
            last = mid
    return first

arr = [1, 2, 2, 3, 4, 5, 5, 5, 7]
bi_search(arr, 2)

```

Decipher on the implementation:

### boundary check

Firstly, boundary check and if there's no satisfactory number exists in given array, we may stop early.

### sector 1

Now come to the search part, in sector 1:
We loop from left to right of an array, if you remember we usually for things like this:

for (i = 0; i < len; i++)

And here is an intelligible explanation:
[Why numbering should start at zero](https://www.cs.utexas.edu/users/EWD/transcriptions/EWD08xx/EWD831.html)

### sector 2
About the mid-point part,

mid = l + (r - l)//2

There's an alternative way:

mid = (l + r)//2

This is also work for python, but will put an adverse effect on stack over flow in c and java, because l + r might cross memory boundary when these 2 numbers are big enough.

And why //2 instead of /2 in python, in python 3, / is the operator to floating-point division and // is to integer division.

### sector 3

Here, we start with:

arr[mid] < n instead of arr[mid] > n

It also implies with our initial logic, let the program search from left/first to right/last, by assuming arr[mid] < n, step by step, moves the search scale.

### sector 4

Why using:

first = mid +1 instead of first = mid here?

Avoid the situation of dead loop. Consider when will the " while first < last " condition always be true (aka dead loop)?

The answer is, when:

first = last = mid

The binary search procedure is to squeeze the search space of [first, last), once the process managed to squeeze the elements between first and last, into one, and by coincidence the element is bigger than given n, the program will trapped into dead loop, and this happens.

With first = mid + 1 been given, this situation will be avoided. And the program ends when first == last, search scale becomes to [first, last), at this moment, returns first or last doesn't matter, they share the same value.

Following are 2 other implementations.

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