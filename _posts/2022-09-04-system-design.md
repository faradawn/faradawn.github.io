---
title: "System design"
layout: post
categories: algo
---

## Part 1 - Design an iterator to flatten nestedList

### Method 1: use dfs to traverse all the leaf of a M-way tree
- Put in vector and build a vector iterator


```c++
class NestedIterator {
public:
    vector<int>::iterator it;
    vector<int>::iterator end;
    vector<int>res;
    
    NestedIterator(vector<NestedInteger> &nestedList) {
        for(NestedInteger& list : nestedList){
            dfs(list);
        }
        it = res.begin();
        end = res.end();
    }
    
    void dfs(NestedInteger& root){
        if(root.isInteger()){
            res.push_back(root.getInteger());
        }else{
            for(NestedInteger& list : root.getList()){
                dfs(list);
            }
        }
    }
    
    int next() {
        int a = *it;
        it++;
        return a;
    }
    
    bool hasNext() {
        return it < end;
    }
};
```

### Method 2: remove first integer 
- Using stack to optimize 

```c++
class NestedIterator {
public:
    stack<vector<NestedInteger>::iterator>begins;
    stack<vector<NestedInteger>::iterator>ends;
    
    NestedIterator(vector<NestedInteger> &nestedList) {
        begins.push(nestedList.begin());
        ends.push(nestedList.end());
    }
    
    int next() {
        return (begins.top()++)->getInteger();
    }
    
    bool hasNext() {
        while(!begins.empty()){
            if(begins.top() == ends.top()){
                begins.pop();
                ends.pop();
            }else{
                vector<NestedInteger>::iterator x = begins.top();
                if((*x).isInteger()){
                    return true;
                }else{
                    begins.top()++;
                    begins.push((*x).getList().begin());
                    ends.push((*x).getList().end());
                }
            }
        }
        return false;
    }
};
```

## Part 2 - Constant time delete 
- [380. Insert Delete GetRandom O(1)](https://leetcode.com/problems/insert-delete-getrandom-o1/)
    - Swap the desired element to vector's end to pop_back
    - Use a map to track the index


## Part 3 - Bit map for repeated alphabets
```c++
class Solution {
public:
    int partitionString(string s) {
        int cnt = 1;
        int bitMap = 0;
        
        for(int i = 0; i < s.length(); i++){
            int n = s[i] - 'a';
            if(bitMap & (1 << n)){
                bitMap = 0;
                cnt ++;
            }
            bitMap = bitMap | (1 << n);
        }   
        return cnt;
    }
};
```