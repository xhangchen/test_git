离散化+差分数组：先离散化把值域范围缩小，然后用差分数组+前缀和计算各个日期的
```cpp
class Solution {
public:
    vector<int> fullBloomFlowers(vector<vector<int>> &flowers, vector<int> &people) {
        vector<int> s;
        for (auto &x: flowers) {
            s.push_back(x[0]);
            s.push_back(x[1]);
        }
        for (auto x: people)
            s.push_back(x);
        sort(s.begin(), s.end());
        s.erase(unique(s.begin(), s.end()), s.end());
        int m = s.size();
        vector<int> a(m + 1);
        for (auto &x: flowers) {
            a[lower_bound(s.begin(), s.end(), x[0]) - s.begin()]++;
            a[lower_bound(s.begin(), s.end(), x[1]) - s.begin() + 1]--;
        }
        for (int i = 1; i <= m; i++)
            a[i] += a[i - 1];
        vector<int> res;
        for (auto x: people)
            res.push_back(a[lower_bound(s.begin(), s.end(), x) - s.begin()]);
        return res;
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY4NjMxNzEzNSwtMTUwMjcxOTc1MiwtMT
M0MzUwNjUxNSwtMjA4ODc0NjYxMiwtMTUwMzQxMjAyOSwtODM3
NjUxNzQ2LC01Mjc3OTU0NTQsLTgzODAzMzg5MCwtMTkyMjk2Mz
E3MCwxMjM3MjkyMTg1LDE3NzYwMTExMDMsODMzMTgxODk3LDE4
NTY4MjgyOTFdfQ==
-->