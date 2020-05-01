---
layout: post
title: "[Algorithm/HackerRank] Sorting - Fraudulent Activity Notifications"
date: 2020-04-16 02:09:10 +0900
categories: 
    - Algorithm
tags:
    - Algorithm
    - HackerRank
    - Sorting
toc: true
---

<!-- more -->


## Probleam
HackerLand National Bank has a simple policy for warning clients about possible fraudulent account activity. If the amount spent by a client on a particular day is greater than or equal to `2x` the client's median spending for a trailing number of days, they send the client a notification about potential fraud. The bank doesn't send the client any notifications until they have at least that trailing number of prior days' transaction data.

Given the number of trailing days `d` and a client's total daily expenditures for a period of `n` days, find and print the number of times the client will receive a notification over all `n` days.

For example, `d=3` and `expenditures = [10, 20, 30, 40, 50]`. On the first three days, they just collect spending data. At day `4`, we have trailing expenditures of `[10, 20, 30]`. The median is `20` and the day's expenditure is `40`. Because `40 >= 2 x 20`, there will be a notice. The next day, our trailing expenditures are `[20, 30, 40]` and the expenditures are `50`. This is less than  so no notice will be sent. Over the period, there was one notice sent.

**Note:** The median of a list of numbers can be found by arranging all the numbers from smallest to greatest. If there is an odd number of numbers, the middle one is picked. If there is an even number of numbers, median is then defined to be the average of the two middle values.

## Function Description
Complete the function activityNotifications in the editor below. It must return an integer representing the number of client notifications.

activityNotifications has the following parameter(s):
- expenditure: an array of integers representing daily expenditures
- d: an integer, the lookback days for median spending

## Input Format
The first line contains two space-separated integers `n` and `d`, the number of days of transaction data, and the number of trailing days' data used to calculate median spending.
The second line contains `n` space-separated non-negative integers where each integer `i` denotes `expenditure[i]`.

## Output Format
Print an integer denoting the total number of times the client receives a notification over a period of  days.


### Constraints

### Sample Input 1
```

9 5
2 3 4 2 3 6 8 4 5
```


### Sample Output 1
```

2
```


## Code

```python
#!/bin/python3

import math
import os
import random
import re
import sys

"""
정수로 이루어진 리스트(정렬이 안된 숫자) A = [2, 3, 1, 4] / B = [4, 7, 7, 8, 9] 가 있을 때 각각 범위가 A는 4, B는 5일 때
범위가 짝수인 경우 가운데 두개의 평균, 홀수인 경우 가운데 자리를 구해야 할때
각 리스트를 인덱스에 +1을 해서 구할 수 있다. (여기서는 배열 9개의 공간에 생성 하겠음)
[A의 경우]                     1  2  3  4  5  6  7  8  9  
A = [2, 3, 1, 4]        ->  [1  1  1  1  0  0  0  0  0]
[B의 경우]
B = [4, 7, 7, 8, 9]     ->  [0  0  0  1  0  0  2  1  1]
그리고 우측에 누적합이 저장된 배열을 counter로 칭하겠다.
이때 counter를 반복하고 value를 어느 변수에 저장하고 해당 변수의 값이 범위(A의 범위는4, B의 범위는5)를 2로 나누어 몫이 큰 시점이
중간 값(Median) 이다.
"""
def getMedian(counter, d):

    count = 0
    median = 0
    for i in range(201): # 201인 이유는 activityNotificiations함수내 counter 선언시 201까지 했으므로
        count += counter[i]
        if count > d//2:  # 2의 몫을 구하는 이유는 가운데 값을 찾기위해 이진탐색을 했기 때문
            median = i  # 이때가 median 이다.
            break
    
    # 짝수 홀수 판단
    if d % 2 == 1:
        # 홀수는 그냥 곱하기 2만 하면됨
        return median*2
    else:
        # 짝수는 가운데 두개의 평균값을 구하는 것임
        # counter의 인덱스는 오름차순이므로 두개의 평균값을 구하기 위해서는 좌측을 골라야한다.
        # 왜? -> 범위가 4이고 리스트가 [1, 2, 3, 4] 일 때 배열로 표시하면 [0 1 1 1 1] 이다.
        #       이때 범위의 중간값을 구하기위해서는 범위가 4이고 이진탐색이므로 반복을 하게되면 배열 [0 1 1 1 1]에서 값을 
        #       하나 씩 더할때 index 3번 째 위치에서 중단하게된다. 그리고 3번째의 위치는 숫자 3이지만 2를 찾기위해서는 왼쪽이므로
        #       아래의 수식이 들어간다.
        for left in range(median, -1, -1):
            count -= counter[left]
            if count < d//2:
                return left + median

"""
정보수집일(d)이 5인경우 매 일자별 지출금액이 expenditure(2 3 4 2 3 6 8 4 5) 일때
초과금액에 대해서 알림을 표시한다.
    단, 초과금액은 정보수집일의 중간값이다,(정보수집일이 5이므로 정보수집일에서 지출된 금액을 오름차순 후 해당 금액의 중간금액이 중간값)
        -> 즉, 1 2 3 4 5 일땐 3이 중간값 1 2 3 4 5 6 일때에는 3+4/2 가 중간값
2 3 4 2 3 6 8 4 5 에서 정보수집일이 5이므로 초기 2 3 4 2 3 을 정렬하면 2 2 3 3 4 이다.
이때 중간값은 3이므로 그다음 금액 6이 중간값x2 보다 크거나 같은경우 알림을 때린다. -> 6 >= 3x2 True 이므로 알림 count += 1
다음 중간값은 3 4 2 3 6 인데 정렬하면 2 3 3 4 6 이고 중간값은 3이므로 다음 금액 -> 8 >= 3x2 True 이므로 알림 count+= 1
다음 중간값은 4 2 3 6 8 인데 정렬하면 2 3 4 6 8 이고 중간값은 4이므로 다음 금액 -. 4 >= 4x2 False 이므로 알림은 하지 않는다.
...
"""
def activityNotifications(expenditure, d):
    # expenditure 는 200 이하라고 함

    count = 0
    counter = [0] * 201 # 중간값을 구할 때 정렬이 필요한데 매 정렬을 하게되면 TimeOut에 걸림

    # expenditure에서 받은 값에서 첫 회전의 d 만큼 counter에 두자
    for exp in expenditure[:d]:
        counter[exp] += 1

    for i in range(d, len(expenditure)):
        front_day = expenditure[i-d]
        back_day = expenditure[i]

        # 중간값 구하기
        # median = sorted(expenditure[i:i+d]) 로해서 홀수이면 짝수 판단을 할 수도 있지만
        # sorted에서 TimeOut 발생가능
        # -> 이미 정렬을 한 이후에 각 가격이 들어간 인덱스(counter)를 생성했으므로 이를 이용하자.
        median = getMedian(counter, d)

        # 정보 수집일 이후 금액이 중간값 이상인지 판단
        if median<=back_day:
            count += 1

        # meidan을 구하기위해서 counter배열을 사용했는데
        # 이는 한자리 씩 증가하므로 아래와 같이 사용
        counter[front_day] -= 1
        counter[back_day] += 1

    return count

    


if __name__ == '__main__':
    # fptr = open(os.environ['OUTPUT_PATH'], 'w')

    # nd = input().split()

    # n = int(nd[0])

    # d = int(nd[1])

    # expenditure = list(map(int, input().rstrip().split()))

    # result = activityNotifications(expenditure, d)
    result = activityNotifications([2, 3, 4, 2, 3, 6, 8, 4, 5], 5)
    # result = activityNotifications([1, 2, 3, 4, 4], 4)
    # result = activityNotifications([2, 3, 4, 2, 3, 6, 8, 4, 5], 5)

    # fptr.write(str(result) + '\n')

    # fptr.close()
```
