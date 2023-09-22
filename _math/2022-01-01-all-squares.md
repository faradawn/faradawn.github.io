---
title: "Math: find all squares/rectangles given n points"
layout: post
---

## Part 0 - Check power of two
```c++
n & (n-1) == 0
```

## Part 1 - Geek: count RB possible ways
- [Geek: Ball Coloring](https://practice.geeksforgeeks.org/problems/ball-coloring3450/1)
- First part is 0 RB/BR pair: RRRR, BBBB
- Second part is 1 RB/BR pair: RBBBBB, RRBBBB, RRRBBB ... (n-1) * 2 -- like sliding window
- Third part is 2 RB/BR pair: RBRRRR, RBBRRR, RBBBRR, ... (n-1) * (n-2) -- like two for loop

```c++
unsigned long long int noOfWays(unsigned long long int n){
    return 2 + 2*(n-1) + (n-1)*(n-2);
}
```

## Part 2 - Finding squares and rectangles
- Finding all possible rectangles

```c++
int countRectangles(vector<vector<int>>& ob){
    set<vector<int> > myset;
 
    // Inserting the pairs in the set
    for (int i = 0; i < ob.size(); ++i) {
        myset.insert(ob[i]);
    }
 
    int ans = 0;
    for (int i = 0; i < ob.size(); ++i)
    {
        for (int j = 0; j < ob.size(); ++j){
            // must be diagonal points
            if (ob[i][0] != ob[j][0] and ob[i][1] != ob[j][1]){   
                // Searching the pairs in the set
                if (myset.count({ ob[i][0], ob[j][1] }) and myset.count({ ob[j][0], ob[i][1]})){
                    ++ans;
                }
            }
        }
    }
 
    return ans / 4;
}
```

- Finding all possible squares
- in [this post](https://leetcode.com/problems/valid-square/discuss/2563726/C%2B%2B-a-general-solution-to-finding-all-squares-given-n-points)

```c++
class Solution {
public:
    bool validSquare(vector<int>& p1, vector<int>& p2, vector<int>& p3, vector<int>& p4) {
        vector<vector<int>> points = {p1, p2, p3, p4};
		
		// add the points into a set
        set<vector<int>> myset;
        for(vector<int> pt : points){
            myset.insert(pt);
        }
        
		// results stores all the squares can construct
        vector<vector<vector<int>>> results;
        
        for(int i = 0; i < points.size(); i++){
            for(int j = i+1; j < points.size(); j++){
				// if two points are the same, skip
                if(points[i][0] == points[j][0] and points[i][1] == points[j][1]){
                    continue;
                }
				
				// create the other pair of diagonal points 
                vector<vector<int>> res = createDiag(points[i], points[j]);
				
				// if the result has decimals, discard
                if(res.size() != 2) continue; 
				
				// if both diagonal points are in the set, we found a square 
                if(myset.find(res[0]) != myset.end() and myset.find(res[1]) != myset.end()){
                    results.push_back({res[0], res[1], points[i], points[j]});
                }
            }
        }
		
		// divide by two because we double counted the same squares formed by different diagonals
        return results.size()/2 > 0;
        
    }
    
    vector<vector<int>> createDiag(vector<int>& a, vector<int>& c){
        double midX = (a[0] + c[0])/2.0;
        double midY = (a[1] + c[1])/2.0;
        
        double bx = midX - (a[1] - midY);
        double by = midY + (a[0] - midX);
        double dx = midX - (c[1] - midY);
        double dy = midY + (c[0] - midX);
        
		// we discard the non-integer points
        double intpart;
        if(modf(bx, &intpart) != 0 or modf(by, &intpart) != 0 or modf(dx, &intpart) != 0 or modf(dy, &intpart) != 0){
            return \{\{\}\}    
        }
        return \{\{(int)bx, (int)by\}, \{(int)dx, (int)dy\}};
    }
};
```

## Hudson Q1

```c++
vector<bool> solution(vector<long long> A) {
    long long a = 1;
    long long b = 1;
    long long c = a + b;
    
    long long maxEle = 0;
    for(long long i : A){
        if(i > maxEle) maxEle = i;
    }
    
    maxEle ++;
    unordered_set<long long> myset;
    myset.insert(a);
    myset.insert(b);
    while(1){
        c = a + b;
        a = b;
        b = c;
        myset.insert(c);
        if(c > maxEle) break;
    }
    
    vector<bool> res(A.size(), false);
    for(int k = 0; k < A.size(); k++){
        long long num = A[k];
        for(long long i = 1; i < num; i++){
            if(myset.find(i) != myset.end() and myset.find(num - i) != myset.end()){
                res[k] = true;
                break;
            } 
        }
    }
    
    return res;
}
```

## Hudson Q2

```py
import pandas as pd
import csv

df = pd.read_csv("/root/customers/data.csv")

print("Total customers:")
print(df.shape[0])

print("Customers by city:")
cities = df['CITY'].value_counts().sort_index()
for name, val in cities.iteritems():
    print(name, ': ', val, sep='')

print("Customers by country:")
cities = df['COUNTRY'].value_counts().sort_index()
for name, val in cities.iteritems():
    print(name, ': ', val, sep='')


print("Country with the largest number of customers' contracts:")
countries = df['COUNTRY'].unique()
maxName = ""
maxCnt = 0
for val in countries:
    curCnt = df.loc[df['COUNTRY'] == val, 'CONTRCNT'].sum()
    if curCnt > maxCnt or (curCnt == maxCnt and val > maxName):
        maxCnt = curCnt
        maxName = val
        
print(maxName, ' (', maxCnt, ' contracts)', sep='')


print("Unique cities with at least one customer:")
print(len(df['CITY'].unique()))
```


## Hudson Q3
```c++
vector<vector<int>> createDiag(vector<int>& a, vector<int>& c){
    double midX = (a[0] + c[0])/2.0;
    double midY = (a[1] + c[1])/2.0;
    
    double bx = midX - (a[1] - midY);
    double by = midY + (a[0] - midX);
    double dx = midX - (c[1] - midY);
    double dy = midY + (c[0] - midX);
    
    double intpart;
    if(modf(bx, &intpart) != 0.0 or modf(by, &intpart) != 0.0 or modf(dx, &intpart) != 0.0 or modf(dy, &intpart) != 0.0){
        return \{\{\}\};
    }
    
    return \{\{(int)bx, (int)by\}, \{(int)dx, (int)dy\}};
}


long long solution(vector<int> x, vector<int> y) {
    vector<vector<int>> points;
    for(int i = 0; i < x.size(); i++){
        points.push_back({x[i], y[i]});
    }
    
    set<vector<int>> myset;
    for(vector<int> vec : points){
        myset.insert(vec);
    }
    
    long long ans = 0;
    
    for(int i = 0; i < points.size(); i++){
        for(int j = i + 1; j < points.size(); j++){
            if(points[i][0] == points[j][0] and points[i][1] == points[j][1]){
                continue;
            }
            
            vector<vector<int>> res = createDiag(points[i], points[j]);
            if(res.size() != 2) continue;
            if(myset.find(res[0]) != myset.end() and myset.find(res[1]) != myset.end()){
                ans ++;
            }
        }
    }
    
    return ans / 2;
}
```


## Hudson Q4
```c++
bool checkDot(vector<int>& a, vector<int>&b, vector<int>& c){
    return (b[0]-a[0]) * (c[0]-a[0]) + (b[1]-a[1]) * (c[1]-a[1]) == 0;
}

long long solution(vector<int> x, vector<int> y) {
    vector<vector<int>> points;
    for(int i = 0; i < x.size(); i++){
        points.push_back({x[i], y[i]});
    }
    
    long long ans = 0;
    
    for(int a = 0; a < points.size(); a++){
        for(int b = a+1; b < points.size(); b++){
            for(int c = b+1; c < points.size(); c++){
                for(int d = c+1; d < points.size(); d++){
                    if(checkDot(points[a], points[b], points[c]) and checkDot(points[b], points[a], points[d]) and checkDot(points[d], points[b], points[c]) and checkDot(points[c], points[a], points[d])){
                        ans ++;
                    }
                }
            }
        }
    }
    
    return ans;
}

// counts only rectangles parallel to axies
// long long solution(vector<int> x, vector<int> y) {
//     vector<vector<int>> points;
//     set<vector<int>> myset;
//     long long ans = 0;
    
//     for(int i = 0; i < x.size(); i++){
//         points.push_back({x[i], y[i]});
//         myset.insert({x[i], y[i]});
//     }
    
//     for(int i = 0; i < points.size(); i++){
//         for(int j = 0; j < points.size(); j++){
//             if(points[i][0] != points[j][0] and points[i][1] != points[j][1]){
//                 if(myset.find({points[i][0], points[j][1]}) != myset.end() and myset.find({points[j][0], points[i][1]}) != myset.end()){
//                     ans ++;
//                 }
//             }
//         }
//     }
    
//     return ans / 4;
// }
```