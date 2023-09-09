拓扑排序模板题
```cpp
class Solution {  
public:  
    bool canFinish(int numCourses, vector<vector<int>> &prerequisites) {  
        vector<int> sub[numCourses];  
        vector<int> in_degree(numCourses);  
        for (auto &e: prerequisites) {  
            sub[e[1]].push_back(e[0]);  
            in_degree[e[0]]++;  
        }  
        queue<int> q;  
        for (int i = 0; i < numCourses; i++)  
            if (!in_degree[i])  
                q.push(i);  
        int cnt = 0;  
        while (!q.empty()) {  
            int t = q.front();  
            q.pop();  
            cnt++;  
            for (auto j: sub[t])  
                if (--in_degree[j] == 0)  
                    q.push(j);  
        }  
        return cnt == numCourses;  
    }  
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTUyNzc5NTQ1NCwtODM4MDMzODkwLC0xOT
IyOTYzMTcwLDEyMzcyOTIxODUsMTc3NjAxMTEwMyw4MzMxODE4
OTcsMTg1NjgyODI5MV19
-->