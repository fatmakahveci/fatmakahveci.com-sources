---
title: Dynamic Programming (DP)
description: Dynamic Programming (DP)
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "coding"
  - "algorithms"
  - "data structures"
comments: true
---
- A technique for efficiently implementing a recursive algorithm by storing partial results
- It starts with a recursive algorithm or definition.
- How to solve a DP problem
  1. The problem can be broken down into "overlapping subproblems"-smaller versions of the original problem that are reused multiple times.
  2. The problem has an "optimal substructure"-an optimal solution can be formed from optimal solutions to the overlapping subproblems of the original problem.

## Implementing a DP algorithm

### 1. Bottom-up (Tabulation)

- It is implemented with iteration and starts at the base cases.
- It is implemented with nested loops and an array.

```pseudo
F = array of length (n + 1)
F[0] = 0
F[1] = 1
for i from 2 to n:
    F[i] = F[i - 1] + F[i - 2]
```

### 2. Top-down (Memoization)

- It is implemented with recursion and made efficient with memoization.
- It is implemented with a recursive function and hash map.
- _Memoizing a result_ means storing the result of a function call, usually in a hashmap or an array, so that when the same function call is made again, we can simply return the memoized result instead of recalculating the result.

```pseudo
memo = hashmap
Function F(integer i):
    if i is 0 or 1:
        return i
    if i doesn't exist in memo:
        memo[i] = F(i - 1) + F(i - 2)
    return memo[i]
```

### Bottom-up vs. top-down

- Bottom-up
  - usually smaller space complexity and faster runtime, as iteration does not have the overhead that recursion does.
  - We need to go through a logical ordering of solving subproblems.
- Top-down
  - easy to write
  - Ordering of subproblems does not matter with recursion.

## How to convert the top-down solution to the bottom-up

- Initialize an array `dp` that is sized according to your state variables. For example, 2D-array for `nums` and `k`.
- If it asks for the max (min) of sth, set the values $-\infty$ ($\infty$).
- Set your base cases, the same as the top-down function.
- Write a for loop that iterates over the state variables. If you have multiple states, you will need to be nested for loops. These loops should start iterating from the base cases.
- Each iteration of the innermost loop represents a given state and is equivalent to a function call to the same state in top-down.
- Return the answer to the original problem.

## How to solve a DP problem

(1) A function or data structure that will compute/contain the answer to the problem for every given state.

- When designing the function/array, we need to decide on _state variables_ to pass as arguments.

- Common state variables:
  1. An index along some input, $i$.
  2. A second index along some input, $j$.
  3. Explicit numerical constraints are given in the problem, $k$.
  4. Variables that describe statuses in a given state. i.e. "true if currently holding a key, false if not", "currently holding $k$ packages" etc.
  5. Some sort of data like a tuple or bitmask used to indicate things being "visited" or "used". "bitmask is a mask where the $i_{th}$ bit indicates if the $i_{th}$ city has been visited".

- i.e. House Robber Problem
  - The only state variable is an integer $i$, which indicates the index of a house.
  - If the problem had an added constraint such as "you are only allowed to rob up to $k$ houses", then $k$ would be another necessary state variable.

(2) A recurrence relation to transition between states.

- A recurrence relation is an equation that relates different states with each other.
- It is closer to our natural way of thinking.
- Start to think about a general state ($i_{th}$) and use information from the problem description to think about how other states relate to the current one.

(3) Base cases, so that our recurrence relation doesn't go on infinitely.

## Time and space complexity

- Time complexity is directly tied to the number of possible states.
- If computing each state requires $F$ time, and there are $n$ possible states, then the time complexity of a DP algorithm is $O(nF)$.
- Computing a state has just been using a recurrence relation equation, which is $O(1)$. Therefore, the time complexity has just been equal to the number of states. To find the number of states, look at each of your state variables, compute the number of values each one can represent, and then multiply all these numbers together.

---

## Ordered partition

---

## Approximate string match

### Longest common substring

```python
def longestCommonSubstring(text1: str, text2: str) -> int:
    m, n = len(text1), len(text2)
    dp_matrix = [ [0] * (n+1) for _ in range(m+1) ]
    max_len = 0
    for col in range(1, n+1):
        for row in range(1, m+1):
            if text1[row-1] == text2[col-1]:
                dp_matrix[row][col] = dp_matrix[row-1][col-1]+1
                max_len = max(max_len, dp_matrix[row][col])
            else:
                dp_matrix[row][col] = max(dp_matrix[row-1][col], dp_matrix[row][col-1])

    return max_len

print(longestCommonSubstring("money", "monkey"))
```

### Edit distance

```python
def edit_distance(word1, word2):
    m = len(word1)
    n = len(word2)

    edit_distance_matrix = [ [0] * (n + 1) for i in range(m + 1) ]

    for row in range(m + 1):
        for column in range(n + 1):
            if row == 0:
                edit_distance_matrix[row][column] = column
            elif column == 0:
                edit_distance_matrix[row][column] = row
            elif word1[row - 1] == word2[column - 1]:
                edit_distance_matrix[row][column] = edit_distance_matrix[row - 1][column - 1]
            else:
                edit_distance_matrix[row][column] = 1 + min(edit_distance_matrix[row][column - 1],
                                                            edit_distance_matrix[row - 1][column],
                                                            edit_distance_matrix[row - 1][column - 1])
    return edit_distance_matrix[m][n]

print(edit_distance("MONKEY", "MONEY"))
```

#### Brute force

- Time Complexity: $O(3^n)$ (In the worst case, we have three choices for every step.)

```pseudo
int editDistance(String word1, String word2) {
    if (word1 == null || word1.length() == 0) 
        return word2.length()
    if (word2 == null || word2.length() == 0) 
        return word1.length()
    return match(word1, word2, 0, 0)
}

int match(String s1, String s2, int i, int j) {
    //If one of the string's pointer has reached the end of it
    if (s1.length() == i)
         return s2.length() - j
    if (s2.length() == j)
        return s1.length() - i
    int result
    // If current position is the same.
    if (s1[i] == s2[j]) {
        result = match(s1, s2, i + 1, j + 1)
    } else {
        //Case1: insert
        int insert = match(s1, s2, i, j + 1)
        //Case2: delete
        int delete = match(s1, s2, i + 1, j)
         //Case3: substitute
        int substitute = match(s1, s2, i + 1, j + 1)
        result = min(insert, delete, substitute) + 1
    }
    return result
}
```

```cpp
row_init(int i) {
    m[0][i].cost = i;
    if (i>0)
        m[0][i].parent = INSERT;
    else
        m[0][i].parent = -1;
}
```

### Special cases of edit distance

#### Substring matching

- Find where a short pattern `P` best occurs within a long text `T`
  - Search for "Skiena" in all its misspellings (Skienna, Skena, Skina, . . . ) within a long file.

```cpp
void row_init(int i, cell m[MAXLEN+1][MAXLEN+1]) { 
    m[0][i].cost = 0; 
    m[0][i].parent = -1;
}
```

#### Longest common subsequence

- Find the longest scattered string of characters included within both strings, without changing their relative order.
  - i.e. `LCS(“democrats", "republicans") = "ecas"`

```cpp
int match(char c, char d) {
    if (c == d) {
        return(0);
    }
    return(MAXLEN);
  }
```

#### Maximum monotone subsequence

- Seek to delete the fewest number of elements from an input string `S` to leave a monotonically increasing subsequence
  - i.e. `MMS(243517698) = 23568`

---

## Longest increasing subsequence

```python
from typing import List

def len_of_lis(nums: List[int]) -> int:
    dp = [1] * len(nums)
    for i in range(1, len(nums)):
        for j in range(i):
            if nums[i] > nums[j]:
                dp[i] = max(dp[i], dp[j] + 1)

    return max(dp)

nums = [10,9,2,5,3,7,101,18]
print(len_of_lis(nums))
```

---

## Parsing context-free grammar

---

## Subset sum

```python
def isSubsetSum(arr, n, sum, dp):

 if sum_ == 0:
  return True
 if n == 0 and sum_ != 0:
  return False

 if dp[n][sum_] != -1:
  return dp[n][sum_]

 if arr[n - 1] > sum_:
  return isSubsetSum(arr, n - 1, sum_, dp)

 dp[n][sum_] = isSubsetSum(arr, n - 1, sum_, dp) or isSubsetSum(arr, n - 1, sum_ - arr[n - 1], dp)

 return dp[n][sum_]

def findPartition(arr, n):
 sum_ = 0
 for i in range(n):
  sum_ += arr[i]
 if sum_ % 2 != 0:
  return False

 dp = [[-1]*(sum_+1)]*(n+1)

 return isSubsetSum(arr, n, sum_ // 2, dp)

arr = [ 3, 1, 5, 9, 12 ]
n = len(arr)

if findPartition(arr, n):
 print("Can be divided into two subsets of equal sum")
else:
 print("Can not be divided into two subsets of equal sum")

arr2 = [ 3, 1, 5, 9, 14 ]
n2 = len(arr2)

if findPartition(arr2, n2):
 print("Can be divided into two subsets of equal sum")
else:
 print("Can not be divided into two subsets of equal sum")
```
