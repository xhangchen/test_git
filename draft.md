$bfs$ : 首先建图：存在边$u$
```cpp
class Solution {
public:
    vector<bool> checkIfPrerequisite(int numCourses, vector<vector<int>> &prerequisites, vector<vector<int>> &queries) {
        vector<int> e[numCourses];
        for (auto &pi: prerequisites)
            e[pi[1]].push_back(pi[0]);
        vector<int> vis(numCourses, -1);
        int is[numCourses][numCourses];
        memset(is, 0, sizeof(is));
        for (int i = 0; i < numCourses; i++) {
            queue<int> q;
            q.push(i);
            vis[i] = i;
            while (!q.empty()) {
                int cur = q.front();
                q.pop();
                for (auto j: e[cur])
                    if (vis[j] != i) {
                        vis[j] = i;
                        is[j][i] = 1;
                        q.push(j);
                    }
            }
        }
        vector<bool> res;
        for (auto &qi: queries)
            res.push_back(is[qi[0]][qi[1]]);
        return res;
    }
};
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTYwNjIyNTE5NiwtODM3NjUxNzQ2LC01Mj
c3OTU0NTQsLTgzODAzMzg5MCwtMTkyMjk2MzE3MCwxMjM3Mjky
MTg1LDE3NzYwMTExMDMsODMzMTgxODk3LDE4NTY4MjgyOTFdfQ
==
-->