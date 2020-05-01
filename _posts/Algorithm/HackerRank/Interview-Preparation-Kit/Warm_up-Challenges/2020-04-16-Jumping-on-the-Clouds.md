---
layout: post
title: "[Algorithm/HackerRank] Warm_up Challenges - Jumping on the Clouds"
date: 2020-04-16 01:23:03 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Warm_up Challenges
---

<!-- more -->


## Probleam
Emma is playing a new mobile game that starts with consecutively numbered clouds. Some of the clouds are thunderheads and others are cumulus. She can jump on any cumulus cloud having a number that is equal to the number of the current cloud plus `1` or `2`. She must avoid the thunderheads. Determine the minimum number of jumps it will take Emma to jump from her starting postion to the last cloud. It is always possible to win the game.

For each game, Emma will get an array of clouds numbered `0` if they are safe or `1` if they must be avoided. For example, `c=[0, 1, 0, 0, 0, 1, 0]` indexed from `0...6`. The number on each cloud is its index in the list so she must avoid the clouds at indexes `1` and `5`. She could follow the following two paths: `0->2->4->6->` or `0->2->3->4->6`. The first path takes `3` jumps while the second takes `4`.

## Function Description
Complete the jumpingOnClouds function in the editor below. It should return the minimum number of jumps required, as an integer.

jumpingOnClouds has the following parameter(s):

- c: an array of binary integers

## Input FOrmat
The first line contains an integer `n`, the total number of clouds. The second line contains `n` space-separated binary integers describing clouds `c[i]` where `0<= i < n`.

## Output Format
Print the minimum number of jumps needed to win the game.

## Sample Input 1
```

7
0 0 1 0 0 1 0
```


## Sample Output 1
```

4
```


## Sample Input 2
```

6
0 0 0 0 1 0
```


## Sample Output 2
```

3
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

# Complete the jumpingOnClouds function below.
def jumpingOnClouds(c):
	count = 0
	idx = 0

	for i in c:
		# c의 마지막 번째의 위치인 경우 더이상 점프할 곳이 없으므로 break
		if idx >= len(c):
			break

		# 1칸 or 2칸 점프가 가능하므로 분기처리
		try:
			if c[idx+2] == 0:
				count += 1
				idx += 2
			elif c[idx+1] == 0:
				count += 1
				idx += 1
		except:
			try:
				if c[idx+1] == 0:
					count += 1
					idx += 1
			except:
				continue
			
	return count
	
if __name__ == '__main__':
	# fptr = open(os.environ['OUTPUT_PATH'], 'w')

	n = int(input())

	c = list(map(int, input().rstrip().split()))

	result = jumpingOnClouds(c)

	print(result)
	# fptr.write(str(result) + '\n')

	# fptr.close()

```

