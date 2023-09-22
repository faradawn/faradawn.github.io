---
title: "Binary search lower and upperbound"
layout: post
categories: algo
---

## Lower Bound 
```c++
int searchLeft(vector<int>& nums, int target){
    int l = 0;
    int r = nums.size()-1;
    while(l <= r){
        int mid = l + (r-l)/2;
        if(nums[mid] >= target){
            r = mid - 1;
        }else{
            l = mid + 1;
        }
    }
    if(l >= nums.size() or nums[l] != target){
        return -1;
    }else{
        return l;
    }
}
```

## Upper Bound
```c++
int searchRight(vector<int>& nums, int target){
    int l = 0;
    int r = nums.size()-1;
    while(l <= r){
        int mid = l + (r-l)/2;
        if(nums[mid] <= target){
            l = mid + 1;
        }else{
            r = mid - 1;
        }
    }
    
    if(r < 0 or nums[r] != target){
        return -1;
    }else{
        return r;
    }
}
```