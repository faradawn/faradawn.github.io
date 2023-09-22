---
title: "Trie: String Split"
layout: post
categories: algo
---

### 1 - Word Break I (DP)
[139. Word Break I](https://leetcode.com/problems/word-break/discuss/43814/C%2B%2B-Dynamic-Programming-simple-and-fast-solution-(4ms)-with-optimization). Given a string s and a dictionary of strings wordDict, return true if s can be segmented into a space-separated sequence of one or more dictionary words.
```
Input: s = "leetcode", wordDict = ["leet","code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```
Solution:

- `dp[i]` records whether the word before `i` can be split.
- for each `i`, check if any `substr(j, i)` is in `dict` and `dp[j] = 1`. 


---


### 2 - Word Break II (Backtracking)
[140. Word Break II](https://leetcode.com/problems/word-break-ii/). 
Given a string s and a dictionary of strings wordDict, add spaces in s to construct a sentence where each word is a valid dictionary word. Return all such possible sentences in any order.
```
Input: s = "catsanddog", wordDict = ["cat","cats","and","sand","dog"]
Output: ["cats and dog","cat sand dog"]
```

Solution:
- Backtrack from s[0, ...], each time try a dict word with `len`. 
- If word matches, continue match `s[idx + len, ...]`.
- End with `idx == s.length()`


### 3 - 



