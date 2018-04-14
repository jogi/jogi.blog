+++
author = "Vashishtha Jogi"
categories = ["Programming"]
date = 2016-08-09T05:39:00Z
description = "Recently I have been trying to do a lot of reading about some very common CS principles. This is the first of the series of posts that I am going to do covering some very basic sorting algorithms, trees, linked lists, etc."
draft = false
slug = "how-to-implement-mergesort-in-python"
tags = ["Programming"]
title = "How to implement Mergesort in Python"

+++

Recently I have been trying to do a lot of reading about some very common CS principles. This is the first of the series of posts that I am going to do covering some very basic sorting algorithms, trees, linked lists, etc.

Starting with merge sort. Here is a very rudimentary implementation of recursive merge sort in Python (I love Python).

```python
def merge(left, right):
    if not len(left) or not len(right):
        return left or right

    result = []
    i, j = 0, 0
    while (len(result) < len(left) + len(right)):
        if left[i] < right[j]:
            result.append(left[i])
            i+= 1
        else:
            result.append(right[j])
            j+= 1
        if i == len(left) or j == len(right):
            result.extend(left[i:] or right[j:])
            break

    return result

def mergesort(list):
    if len(list) < 2:
        return list

    middle = len(list)/2
    left = mergesort(list[:middle])
    right = mergesort(list[middle:])

    return merge(left, right)

if __name__ == "__main__":
    print mergesort([3,4,5,1,2,8,3,7,6])
```

I am not going to explain the whole merge sort algorithm. [Wikipedia](https://en.wikipedia.org/wiki/Merge_sort) does an excellent job at that.
