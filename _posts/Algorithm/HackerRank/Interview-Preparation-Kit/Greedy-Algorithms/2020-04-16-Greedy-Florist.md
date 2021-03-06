---
layout: post
title: "[Algorithm/HackerRank] Greedy Algorithms - Greedy Florist"
date: 2020-04-16 02:34:22 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Greedy Algorithms
toc: true
---

<!-- more -->


## Probleam
A group of friends want to buy a bouquet of flowers. The florist wants to maximize his number of new customers and the money he makes. To do this, he decides he'll multiply the price of each flower by the number of that customer's previously purchased flowers plus `1`. The first flower will be original price, `(0+1) x original price`, the next will be `(1+1) x original price` and so on.

Given the size of the group of friends, the number of flowers they want to purchase and the original prices of the flowers, determine the minimum cost to purchase all of the flowers.

For example, if there are `k=3` friends that want to buy `n=4` flowers that cost `c=[1, 2, 3, 4]` each will buy one of the flowers priced `[2,3,4]` at the original price. Having each purchased `x = 1` flower, the first flower in the list, `c[0]`, will now cost `(current purchase + previous purchases) x c[0] = (1+1) x 1 = 2`. The total cost will be `2 + 3 + 4 + 2 = 11`.

## Function Description
Complete the getMinimumCost function in the editor below. It should return the minimum cost to purchase all of the flowers.

getMinimumCost has the following parameter(s):
- c: an array of integers representing the original price of each flower
- k: an integer, the number of friends

## Input Format
The first line contains two space-separated integers `n` and `k`, the number of flowers and the number of friends.
The second line contains `n` space-separated positive integers `c[i]`, the original price of each flower.

## Output Format
Print the minimum cost to buy all `n` flowers.

## Sample Input 1
```

3 3
2 5 6
```


## Sample Output 1
```

13
```


## Sample Input 2
```

3 2
2 5 6
```


## Sample Output 2
```

16
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the getMinimumCost function below.
def getMinimumCost(k, c):
    total = 0
    counter = 0
    length = len(c)
    c.sort(reverse=True)

    for i in range(0, length):
        total += (counter + 1) * c[i]
        if length != k and (i + 1) % k == 0:
            counter += 1

    return total

if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # nk = input().split()

    # n = int(nk[0])  # Count of Flowers

    # k = int(nk[1])  # Count of People

    # c = list(map(int, input().rstrip().split()))

    # minimumCost = getMinimumCost(k, c)
    minimumCost = getMinimumCost(2, [2, 5, 6])
    print(minimumCost)
    # fptr.write(str(minimumCost) + '\n')

    # fptr.close()
```
