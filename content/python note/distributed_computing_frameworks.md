---
title: Distributed computing frameworks
description: Distributed computing frameworks
summary: "Updated by Fatma, Mar 28, 2023."
date: 28-03-2023
categories:
  - "Coding"
tags:
  - "Python"
  - "coding"
  - "algorithms"
  - "data structures"
---

Processing truly big datasets with Hadoop and Spark

## Distributed computing

- .

## 1. Hadoop

- It is a set of tools that support distributed maps and reduce style programming through Hadoop MapReduce.
- It is for batch processing of big datasets.
- It uses the distributed file system for storing big data and MapReduce to process it.
- It excels in storing and processing of huge data of various formats such as arbitrary, semi-, or even unstructured.

### `mrjob` library

- It is used to write Hadoop jobs
- Prerequisites:
  - `pip install mrjob`
  - `brew install hadoop`

## 2. Spark

- It is an analytics toolkit designed to modernize Hadoop.
- We will apply Spark in analytics and machine learning use cases.

---

## mapreduce

- `Map` transforms the data by dividing it into key/value pairs, getting the output from a map as an input.
- `Reduce` aggregates data together.
- It is written in Java, but it can run in Python, C++, etc.

```python
import functools
from typing import Dict

def map_frequency(text: str) -> Dict[str, int]:
 frequencies = {}
 for word in text.split(' '): # words
  if word in frequencies:
   frequencies[word] += 1
  else:
   frequencies[word] = 1

 return frequencies

def merge_dictionaries(first: Dict[str, int], second: Dict[str, int]) -> Dict[str, int]:
 merged = first
 for key in second:
  if key in merged:
   merged[key] += second[key]
  else:
   merged[key] = second[key]
 return merged

if __name__ == "__main__":
 lines = [ "I know what I know",
       "I know that I know",
        "I don't know much",
        "They don't know much" ]

 mapped_results = [ map_frequency(line) for line in lines ]

 for result in mapped_results:
  print(result)

 print(functools.reduce(merge_dictionaries, mapped_results))
```
