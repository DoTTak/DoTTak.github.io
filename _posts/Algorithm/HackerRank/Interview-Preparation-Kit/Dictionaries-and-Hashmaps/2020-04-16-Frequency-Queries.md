---
layout: post
title: "[Algorithm/HackerRank] Dictionaries and Hashmaps - Frequency Queries"
date: 2020-04-16 01:55:44 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Dictionaries and Hashmaps
---

> HackerRank의 Interview Preparation Kit 풀이 입니다.

<!-- more -->


## Probleam
You are given `q` queries. Each query is of the form two integers described below:
- `1x` : Insert x in your data structure.
- `2y` : Delete one occurence of y from your data structure, if present.
- `3z` : Check if any integer is present whose frequency is exactly . If yes, print 1 else 0.

The queries are given in the form of a 2-D array `queries` of size `q` where `queries[i][0]` contains the operation, and  contains the data element. For example, you are given array `queries = [(1,1), (2,2), (3,2), (1,1), (1,1), (2,1), (3,2)]`. The results of each operation are:
```

Operation   Array   Output
(1,1)       [1]
(2,2)       [1]
(3,2)                   0
(1,1)       [1,1]
(1,1)       [1,1,1]
(2,1)       [1,1]
(3,2)                   1
```

Return an array with the output: `[0, 1]`.

## Function Description
Complete the freqQuery function in the editor below. It must return an array of integers where each element is a `1` if there is at least one element value with the queried number of occurrences in the current array, or 0 if there is not.

freqQuery has the following parameter(s):

queries: a 2-d array of integers

## Input Format
The first line contains of an integer `q`, the number of queries.
Each of the next `q` lines contains two integers denoting the 2-d array `queries`.

## Output Format
Return an integer array consisting of all the outputs of queries of type `3`.

## Sample Input 1
```

8
1 5
1 6
3 2
1 10
1 10
1 6
2 5
3 2
```


## Sample Output 1
```

0
1
```


## Sample Input 2
```

4
3 4
2 1003
1 16
3 1
```


## Sample Output 2
```

0
1
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the freqQuery function below.
"""
q개의 query가 주어졌을 때, 값에 따라 수행 후 최종 결과 반환
(1<=q<=10^6, 1<=x,y,z<=10^9, q[i][0] ∈ {1,2,3} ,1<=q[i][1]<=10^9)
[1 x] : x 추가
[2 y] : y 하나 제거
[3 z] : z개만큼 있는 수가 있으면 1, 없으면 0
"""
def freqQuery(queries):
    memo = {}
    count_dict = {}
    output = []
    for query in queries:
        cmd = query[0]
        value = query[1]

        if cmd == 1:
            if value in memo.keys():
                
                if memo[value] in count_dict.keys():
                    count_dict[memo[value]] -= 1
                else:
                    count_dict[memo[value]] = -1

                memo[value] += 1
                
                if memo[value] in count_dict.keys():
                    count_dict[memo[value]] += 1
                else:
                    count_dict[memo[value]] = 1

            else:

                memo[value] = 1

                if memo[value] in count_dict.keys():
                    count_dict[1] += 1
                else:
                    count_dict[1] = 1

        elif cmd == 2:
            
            if value in memo.keys():
                
                if memo[value] in count_dict.keys():
                    count_dict[memo[value]] -= 1
                else:
                    count_dict[memo[value]] = -1

                memo[value] = max(memo[value]-1, 0) # 음수가 될 수 없으므로 0기입

                if memo[value] in count_dict.keys():
                    count_dict[memo[value]] += 1
                else:
                    count_dict[memo[value]] = 1


        elif cmd == 3:
            if value in count_dict.keys() and count_dict[value] > 0:
                output.append(1)
            else:
                output.append(0)

    return output

if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # q = int(input().strip())

    # queries = []

    # for _ in range(q):
    #     queries.append(list(map(int, input().rstrip().split())))

    # ans = freqQuery(queries)
    ans = freqQuery([[1, 3], [2, 3], [3, 2], [1, 4], [1, 5], [1, 5], [1, 4], [3, 2], [2, 4], [3, 2]])

    # fptr.write('\n'.join(map(str, ans)))
    # fptr.write('\n')

    # fptr.close()
```
