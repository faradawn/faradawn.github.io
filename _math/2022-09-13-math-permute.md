---
title: "Math: all permutation a string"
layout: post
categories: algo
---

## 1 - Permutations of a string (with duplicates)
```c++
class Solution{
public:
    string onPath;
    vector<string> res;
    vector<int> used;

    void dfs(string s){
        if(onPath.length() == s.length()){
            res.push_back(onPath);
            return;
        }

        for(unsigned i = 0; i < s.length(); i++){
            if(i > 0 and s[i] == s[i-1] and !used[i-1]) continue;
            if(used[i] == 1) continue;
            used[i] = 1;
            onPath = onPath + s[i];
            dfs(s);
            onPath.pop_back();
            used[i] = 0;
        }
    }

    vector<string> permute_string(string s){
        sort(s.begin(), s.end());
        used.resize(s.length(), 0);
        dfs(s);
        return res;
    }
};
```


## 2 - 