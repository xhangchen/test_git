模拟
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
eyJoaXN0b3J5IjpbLTE1MDI3MTk3NTIsLTEzNDM1MDY1MTUsLT
IwODg3NDY2MTIsLTE1MDM0MTIwMjksLTgzNzY1MTc0NiwtNTI3
Nzk1NDU0LC04MzgwMzM4OTAsLTE5MjI5NjMxNzAsMTIzNzI5Mj
E4NSwxNzc2MDExMTAzLDgzMzE4MTg5NywxODU2ODI4MjkxXX0=

-->