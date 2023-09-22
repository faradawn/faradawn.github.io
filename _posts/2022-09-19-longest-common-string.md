---
title: "DP: Longest Common Subsequence"
layout: post
categories: algo
---

## 1 - Longest Common Subarray
> Given two integer arrays nums1 and nums2, return the maximum length of a subarray that appears in both arrays.
```
Input: nums1 = [1,2,3,2,1], nums2 = [3,2,1,4,7]
Output: 3
Explanation: The repeated subarray with maximum length is [3,2,1].
```
Solution: dp O(n^2)

```c++
if(nums1[i] == nums2[j]){
    if(i > 0 and j > 0){
        dp[i][j] = dp[i-1][j-1] + 1;
    }else{
        dp[i][j] = 1;
    }
    if(dp[i][j] > res)
        res = dp[i][j];
}
```

## 2 - Longest common subsequence
```
Input: text1 = "abcde", text2 = "ace" 
Output: 3  
Explanation: The longest common subsequence is "ace" and its length is 3.
```

Solution: dp is longest common subseq of s1[0, i] and s2[0, j]

```c++
if (s1.charAt(i - 1) == s2.charAt(j - 1)) {
    // s1[i-1] 和 s2[j-1] 必然在 lcs 中
    dp[i][j] = 1 + dp[i - 1][j - 1];
} else {
    // s1[i-1] 和 s2[j-1] 至少有一个不在 lcs 中
    dp[i][j] = Math.max(dp[i][j - 1], dp[i - 1][j]);
}
```
