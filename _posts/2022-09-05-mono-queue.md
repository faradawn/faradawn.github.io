---
title: "Monotonic queue: Max for sliding window"
layout: post
categories: algo
---

## Part 1 - Max in sliding window
- Use a monotonic queue O(n)

![mono_queue_max](/assets/img/algo_graphs/max_mono_queue-min.JPG){:width="90%"}

```c++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        // queue of indecies
        deque<int> q;
        vector<int> res;
        for(int i = 0; i < nums.size(); i++){
            // remove outlated indecies
            while(!q.empty() and q.front() <= i - k){
                q.pop_front();
            }
            // remove the smaller elements
            while(!q.empty() and nums[q.back()] < nums[i]){
                q.pop_back();
            }
            
            q.push_back(i);
            if(i - k + 1 >= 0){
                res.push_back(nums[q.front()]);
            }
        }
        
        return res;
    }
};
```

- Multiset method O(nlogn)

```c++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        multiset<int> s;
        for(int i = 0; i < k; i++){
            s.insert(nums[i]);
        }
        vector<int> res;
        res.push_back(*(s.rbegin()));
        for(int i = k; i < nums.size(); i++){
            s.erase(s.find(nums[i-k]));
            s.insert(nums[i]);
            res.push_back(*(s.rbegin()));
        }
        return res;
    }
};
```
