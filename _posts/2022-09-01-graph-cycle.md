---
title: "Graph: cycle detection"
layout: post
categories: algo
---

## Cycle Detection
- [207. Course Schedule](https://leetcode.com/problems/course-schedule/)
```c++
class Solution {
public:
    map<int, vector<int>> adj;
    vector<bool> visited;
    vector<bool> onPath;
    bool hasCycle = 0;
    
    void dfs(int s){
        if(onPath[s] or hasCycle){
            hasCycle = 1;
            return;
        }
        if(visited[s]){
            return;
        }
        visited[s] = 1;
        onPath[s] = 1;
        for(int t : adj[s]){
            dfs(t);
        }
        onPath[s] = 0;
    }
    bool canFinish(int numCourses, vector<vector<int>>& prerequisites) {
        visited.resize(numCourses, 0);
        onPath.resize(numCourses, 0);
        for(vector<int>& vec : prerequisites){
            adj[vec[1]].push_back(vec[0]);
        }
        for(auto&it : adj){
            dfs(it.first);
            if(hasCycle) return false;
        }
        return true;
    }
};
```

## Topological Sort
- [210. Course Schedule II](https://leetcode.com/problems/course-schedule-ii/)
```c++
class Solution {
public:
    map<int, vector<int>> adj;
    vector<bool> visited;
    vector<bool> onPath;
    bool hasCycle = 0;
    vector<int> postarr;
    
    void postorder(int s){
        if(visited[s]){
            return;
        }
        
        visited[s] = 1;
        
        for(int t : adj[s]){
            postorder(t);
        }
        postarr.push_back(s);
    }
    
    vector<int> findOrder(int numCourses, vector<vector<int>>& prerequisites) {
        if(!canFinish(numCourses, prerequisites)) return {};
        
        // clear visited array
        for(int i = 0; i < visited.size(); i++){
            visited[i] = 0;
        }
        
        // post-order traversal 
        for(auto&it : adj){
            postorder(it.first);
        }
        
        // reverse postorder array
        reverse(postarr.begin(), postarr.end());
        
        // push the remaining elements
        for(int i = 0; i < numCourses; i++){
            if(adj.count(i) == 0){
                postarr.push_back(i);
            }
        }
        return postarr;
    }
};
```

## 2D topological sort matrix
- [2392. Build a Matrix With Conditions](https://leetcode.com/problems/build-a-matrix-with-conditions/)
- [Official TopoSort](https://cp-algorithms.com/graph/topological-sort.html#implementation)
```c++
class Solution {
public:
    vector<bool> onPath;
    vector<bool> visited;
    bool hasCycle = false;
    
    void topSort(unordered_map<int, set<int>>& adj, int s, vector<int>& ans) {
        if (onPath[s] or hasCycle) {
            hasCycle = 1;
            return;
        }
        if (visited[s]) {
            return;
        }
        visited[s] = 1;
        onPath[s] = 1;
        for (int t : adj[s]) {
            topSort(adj, t, ans);
        }
        onPath[s] = 0;
        ans.push_back(s);
    }
    
    
    vector<vector<int>> buildMatrix(int k, vector<vector<int>>& rowConditions, vector<vector<int>>& colConditions) {
        unordered_map<int, set<int>> rowAdj;
        unordered_map<int, set<int>> colAdj;
        visited.assign(k+1, 0);
        onPath.assign(k+1, 0);
        
        for(int i = 1; i <= k; i++){
            rowAdj[i] = set<int>();
            colAdj[i] = set<int>();
        }
        for(auto &vec : rowConditions){
            rowAdj[vec[1]].insert(vec[0]);
        }
        for(auto &vec : colConditions){
            colAdj[vec[1]].insert(vec[0]);
        }
        
        vector<vector<int>>res;
        vector<int> postorderR;
        vector<int> postorderC;
        
        for(auto &it : rowAdj){
            topSort(rowAdj, it.first, postorderR);
            if(hasCycle) return res; 
        }
        
        visited.assign(k+1, 0);
        onPath.assign(k+1, 0);
        
        for(auto &it : colAdj){
            topSort(colAdj, it.first, postorderC);
            if(hasCycle) return res; 
        }
        
        map<int, int> mapR;
        
        for(int i = 0; i < postorderR.size(); i++){
            mapR[postorderR[i]] = i;
        }
     
        vector<vector<int>> ans(k, vector<int>(k, 0));
        
        for(int i = 0; i < postorderC.size(); i++){
            ans[mapR[postorderC[i]]][i] = postorderC[i];
        }
        
        return ans;
    }
};
```