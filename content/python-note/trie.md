---
title: Trie
description: Trie
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
- A type of tree
- It stores characters.
- Don't look up each prefix from the root.
  - Build on past calls.

- You can implement it by keeping the state within a tree and return Node reference

```python
class TrieNode:
    def __init__(self):
        self.children = {}
        self.end_of_trie = False

class Trie:
    def __init__(self):
        self.root = TrieNode()
    
    def insert(self, word:str) -> None:
        curr = self.root
        for ch in word:
            if ch not in curr.children:
                curr.children[ch] = TrieNode()
            curr = curr.children[ch]
        curr.end_of_trie = True
    
    def search(self, word: str) -> bool:
        curr = self.root
        for ch in word:
            if ch not in curr.children:
                return False
            curr = curr.children[ch]
        return curr.end_of_trie
    
    def startsWith(self, prefix: str) -> bool:
        curr = self.root
        for ch in prefix:
            if ch not in curr.children:
                return False
            curr = curr.children[ch]
        return True
```
