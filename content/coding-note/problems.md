---
title: Some common problems
description: Some common problems
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
  - "algorithms"
  - "data structures"
comments: true
---
## greatest number less than or equal to the target

```python
def floor(arr, target):

 if target < arr[0]:
  return -1

 low, high = 0, len(arr)-1

 while low <= high:
  mid = (low+high)//2
  if arr[mid] == target:
   return mid
  elif arr[mid] < target:
   low = mid+1
  elif arr[mid] > target:
   high = mid-1

 return high


if __name__ == "__main__":
 print(floor([2, 3, 5, 9, 14, 16, 18], 19))
```

## Clone singly linked list

```python
class Node:
 def __init__(self, data=None, next=None):
  self.data = data
  self.next = next

def print_list(head): 
    ptr = head
    while ptr:
        print(ptr.data, end=" —> ")
        ptr = ptr.next
    print("null")

def copy_list(head):
 if not head:
  return
 new_head = Node(head.data)
 new_head.next = copy_list(head.next)
 return new_head

if __name__ == "__main__":

 head = None
 for i in reversed(range(4)):
  head = Node(i+1, head)
 print_list(head)

 new_head = copy_list(head)
 print(print_list(new_head))
```

## Smallest number greater than or equal to the target

```python
def ceiling(arr, target):

 if target > arr[-1]:
  return -1

 low, high = 0, len(arr)-1

 while low <= high:
  mid = (low+high)//2
  if arr[mid] == target:
   return mid
  elif arr[mid] < target:
   low = mid+1
  elif arr[mid] > target:
   high = mid-1

 return low

if __name__ == "__main__":
 print(ceiling([2, 3, 5, 9, 14, 16, 18], 19))
```

## Change making

```python
"""
Top-down

Time: O(nv), where v is the number of steps. In the worst case, we pay with v coins of value 1.
"""

def make_change(coins: int, amount: float) -> list[int]:

 @lru_cache(maxsize = None)
 def helper(amount):

  if not amount:
   return []

  if amount < 0:
   return None

  optimal_result = None

  for coin in coins:

   partial_result = helper(amount - coin)

   if partial_result is None:
    continue

   candidate = partial_result + [coin]

   if ( optimal_result is None ) or ( len(candidate) < len(optimal_result) ):
    optimal_result = candidate

  return optimal_result

 return helper(amount)

######################################################

"""
Bottom-up

Time: O(nv)
"""

def make_change(coins: int, amount: float) -> list[int]:

 solutions = [None] * (amount + 1)
 solutions[0] = []

 paid = 0
 while paid < amount:

  if solutions[paid] is not None:

   for coin in coins:

    next_paid = paid + coin

    if next_paid > amount:
     continue

    if (solutions[next_paid] is None or len(solutions[next_paid]) > len(solutions[paid]) + 1):
     solutions[next_paid] = solutions[paid] + [coin]

  paid += 1

 return solutions[amount]
```

```python
"""
Bottom-up + BFS

Time: O(nv)
"""

def simplest_change(coins: int, amount: float) -> list[int]:
 solutions = { 0: [] }
 amounts_to_be_handled = collections.deque([0])

 while amounts_to_be_handled:

  paid = amounts_to_be_handled.popleft()
  solution = solutions[paid]
  
  if paid == amount:
   return solution

  for coin in coins:
   next_paid = paid + coin

   if next_paid > amount:
    continue

   if next_paid not in solutions:
    solutions[next_paid] = solution + [coin]
    amounts_to_be_handled.append(next_paid)

 return None
```

---

## Optimal stock

```python
"""
The max profit without any limit

Top-down

Time: O(n)
Space: O(n) with caching
"""

def max_profit(daily_price):

 @lru_cache(maxsize=None)
 def get_best_profit(day, have_stock):

  if day < 0:
   if not have_stock:
    return 0
   else: # initial stock
    return -float('inf')

  price = daily_price[day]

  if have_stock:
   strategy_buy = get_best_profit(day - 1, False) - price
   strategy_hold = get_best_profit(day - 1, True)
   return max(strategy_buy, strategy_hold)
  else:
   strategy_sell = get_best_profit(day - 1, True) + price
   strategy_hold = get_best_profit(day - 1, False)
   return max(strategy_sell, strategy_hold)

 last_day = len(daily_price) - 1
 no_stock = False
 return get_best_profit(last_day, no_stock)

################################################################################

"""
The max profit with a budget limit

Bottom-up (Start from the initial state and iterate day by day until we reach the final state)

Time: O(n)
Space: O(1)
"""

def max_profit(daily_price, budget):

 cash_not_owning_share = budget
 cash_owning_share = -float('inf')

 for price in daily_price:
  strategy_buy = cash_not_owning_share - price
  strategy_hold = cash_owning_share

  strategy_sell = cash_owning_share + price
  strategy_avoid = cash_not_owning_share

  cash_owning_share = max(strategy_buy, strategy_hold)
  if cash_owning_share < 0:
   cash_owning_share = -float('inf')

  cash_not_owning_share = max(strategy_sell, strategy_hold)

 return cash_not_owning_share

################################################################################

"""
The max profit with the limit of total number of transactions

"""

def max_profit(daily_price, tx_limit):

 cash_owning_share = [ -float('inf') ] * (tx_limit + 1)

 cash_not_owning_share = [ -float('inf') ] * (tx_limit + 1)
 cash_not_owning_share[0] = 0

 for price in daily_price:

  cash_not_owning_share_next = [ -float('inf') ] * (tx_limit + 1)
  cash_owning_share_next = [ -float('inf') ] * (tx_limit + 1)

  for prev_tx_count in range(tx_limit):

   strategy_buy = cash_not_owning_share[prev_tx_count] - price
   strategy_hold = cash_owning_share[prev_tx_count]

   strategy_sell = cash_owning_share[prev_tx_count] + price
   strategy_avoid = cash_not_owning_share[prev_tx_count]

  if prev_tx_count < tx_limit:
   cash_not_owning_share_next[ prev_tx_count + 1 ] = max( cash_not_owning_share_next[prev_tx_count + 1],
                   strategy_sell )
 
  cash_not_owning_share_next[prev_tx_count] = max( cash_not_owning_share_next[prev_tx_count],
               strategy_avoid )
  cash_owning_share_next[prev_tx_count] = max( cash_not_owning_share_next[prev_tx_count],
              strategy_buy,
              strategy_hold )
  cash_owning_share = cash_not_owning_share_next

 return max(cash_not_owning_share)
```

---

## Number of expressions with a target result

```python
def count_expressions(numbers, target_result):

 def count(index, partial_result):

  if index == len(numbers):
   if partial_result == target_result:
    return 1
   return 0

  count_add = count(index + 1, partial_result + numbers[index])
  count_sub = count(index + 1, partial_result - numbers[index])

  return count_add + count_sub

 first_index = 1
 partial_result = numbers[0]
 return count(first_index, partial_result)

######################################################################

"""
Top-down

Time: O(nS)
"""

from functools import lru_cache

def count_expressions(numbers, target_result):

 @lru_cache(maxsize=None)
 def count(index, partial_result):

  if index == len(numbers):
   if partial_result == target_result:
    return 1
   return 0

  count_add = count(index + 1, partial_result + numbers[index])
  count_sub = count(index + 1, partial_result - numbers[index])

  return count_add + count_sub

 first_index = 1
 partial_result = numbers[0]

 return count(first_index, partial_result)

######################################################################

"""
Bottom-up - DP + BFS

Time: O(nS)
"""

# HERE
```

---

## Print stars

```python
#!/usr/bin/env python3

####
# def print_stars(n: int) -> None:
#  '''
#  ***
#  ***
#  ***
#  '''
#  for i in range(1, n+1):
#   for j in range(1, n+1):
#    print('*', end='')
#   print()
# print_stars(n=3)
####
# def print_stars(n: int) -> None:
#  '''
#  *
#  **
#  ***
#  '''
#  for i in range(1, n+1):
#   for j in range(1,i+1):
#    print('*', end='')
#   print()
# print_stars(n=3)
####
# def print_stars(n: int) -> None:
#  '''
#  ***
#  **
#  *
#  '''
#  for i in range(1, n+1):
#   for j in range(n+1, i, -1):
#    print('*', end='')
#   print()
# print_stars(n=3)
####
# def print_stars(n: int) -> None:
#  '''
#  1
#  12
#  123
#  '''
#  for i in range(1, n+1):
#   for j in range(1, i+1):
#    print(j, end='')
#   print()
# print_stars(n=3)
####
# def print_stars(n: int) -> None:
#  '''
#  *
#  **
#  ***
#  **
#  *
#  '''
#  for i in range(1, 2*n):
#   number_of_stars = 2*n-i if i > n else i
#   print(''.join(['*']*number_of_stars))
# print_stars(n=3)
####
# def print_stars(n: int) -> None:
#  '''
#    *
#   * *
#  * * *
#   * *
#    *
#  '''
#  for i in range(1, 2*n):
#   number_of_blanks = n-i if i < n else i-n
#   number_of_stars = i if i <= n else 2*n-i
#   print(''.join([' ']*number_of_blanks), ''.join(['* ']*number_of_stars))
# print_stars(n=3)
####
# def print_stars(n: int) -> None:
#  '''
#          1 
#        1 2 1 
#      1 2 3 2 1 
#    1 2 3 4 3 2 1 
#  1 2 3 4 5 4 3 2 1 
#  '''
#  for row in range(1, n+1):
#   for blank in range(1,n+1-row):
#    print(' ', end='')
#   for col in range(1, row):
#    print(str(col), end = '')
#   for col in range(row, 0, -1):
#    print(str(col), end = '')
#   print()

# print_stars(n=5)
####
# def print_stars(n: int) -> None:
#  '''
#  111111111
#  122222221
#  123333321
#  123444321
#  123454321
#  123444321
#  123333321
#  122222221
#  111111111
#  '''
#  for i in range(1, 2*n):
#   for j in range(1, 2*n):
#    print(min(i, j, 2*n-i, 2*n-j),end='')
#   print()
# print_stars(n=5)
####
```
