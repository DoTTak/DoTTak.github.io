---
layout: post
title: "[Algorithm/HackerRank] Sorting - Merge Sort: Counting Inversions"
date: 2020-04-16 02:12:48 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Sorting
---

<!-- more -->


## Probleam
In an array, `arr`, the elements at indices `i` and `j`(where `i<j`) form an inversion if `arr[i] > arr[j]`. In other words, inverted elements `arr[i]` and `arr[j]` are considered to be "out of order". To correct an inversion, we can swap adjacent elements.

For example, consider the dataset `arr = [2,4,1]`. It has two inversions: `(4, 1)` and `(2, 1)`. To sort the array, we must perform the following two swaps to correct the inversions:
```

           swap(arr[1],arr[2]) -> swap(arr[0],arr[1])
arr = [2,4,1] ---------------------------------> [1,2,4]
```

Given `d` datasets, print the number of inversions that must be swapped to sort each dataset on a new line.

## Function Description
Complete the function countInversions in the editor below. It must return an integer representing the number of inversions required to sort the array.

countInversions has the following parameter(s):
- arr: an array of integers to sort .

## Input Format
The first line contains an integer, `d`, the number of datasets.

Each of the next `d` pairs of lines is as follows:

1. The first line contains an integer, `n`, the number of elements in `arr`.
2. The second line contains `n` space-separated integers, `arr[i]`.
Constraints

## Output Format
For each of the `d` datasets, return the number of inversions that must be swapped to sort the dataset.

## Sample Input 1
```

2  
5  
1 1 1 2 2  
5  
2 1 3 1 2
```


## Sample Output 1
```

0
4
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

def merge(arr, temp, counter, left, mid, right):
    left_idx = left     # 왼쪽 배열의 첫 번째 인덱스
    right_idx = mid+1   # 오른쪽 배열의 첫 번째 인덱스
    target_idx = left      # merge할 때 정렬된 위치(인덱스)

    # 실제 배열을 temp 배열에 복사
    for i in range(left, right+1):
        temp[i] = arr[i]
    
    # 왼쪽 리스트는 mid가 마지막이고 
    # 오른쪽 리스트는 right가 마지막이다.
    while left_idx <= mid and right_idx <= right:
        # 합병 정렬에서 실제로 교환이 일어나는 부분은
        # 우측에 있는 값이 좌측에 있는 값 보다 작을 경우
        if temp[left_idx] <= temp[right_idx]:
            arr[target_idx] = temp[left_idx]    # left_idx를 기준으로 하므로
                                                # target_idx에 left_idx를 삽입
            left_idx += 1
        else:
            arr[target_idx] = temp[right_idx]   # right_idx를 기준으로 하므로
                                                # target_idx에 right_idx를 삽입
            right_idx +=1

            """
            1 2 3 1 4 5 가 있을 때 1 2 3 / [1] 4 5 로 Division을 하고
            오른쪽 첫번 째 1을 왼쪽 1 다음으로 이동해야 한다.
            1 [1] 2 3 / 4 5 이때 오른쪽 [1]이 왼쪽 1 다음으로 이동한 거리가 2이므로
            이는 mid - left_idx + 1 로 구한다.
            """
            counter[0] += (mid - left_idx + 1)
        
        target_idx += 1
    
    for i in range(0, mid - left_idx+1):
        arr[target_idx + i] = temp[left_idx + i]


def mergeSort(arr, temp, counter, left, right):
    """
    Merge Sort(병합정렬)
    Left, Right를 각각 division과정을 한 후 다시 Merge
    """
    if left < right:

        # mid 중간값
        mid = (left + right) // 2

        # Division
        mergeSort(arr, temp, counter, left, mid)    # Left
        mergeSort(arr, temp, counter, mid+1, right) # Right

        # Merge
        # 정렬된 Left와 Right를 다시 병합
        merge(arr, temp, counter, left, mid, right)


# Complete the countInversions function below.
def countInversions(arr):
    
    length = len(arr)

    temp = [0] * length # 정렬을 할때 사용할 변수
    counter = [0]       # swap을 계산하는 용도(Call By References)

    # 배열의 left, mid, right를 구함(index)
    # 만일 5개의 배열이 있을경우 [0, 0, 0, 0, 0]
    # left는 0 right는 4(총길이-1)
    left = 0
    right = length-1

    mergeSort(arr, temp, counter, left, right)
    return counter[0]



if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # t = int(input())

    # for t_itr in range(t):
    #     n = int(input())

    #     arr = list(map(int, input().rstrip().split()))

    # result = countInversions(arr)
    result = countInversions([2, 1, 3, 1, 2])
    #     fptr.write(str(result) + '\n')

    # fptr.close()
```
