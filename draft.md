离散化+差分数组：先离散化把值域范围缩小，然后用差分数组+前缀和计算各个日期花的数目
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
        s.erase(unique(s.begin(), s.end()), s.end());//去重
        int m = s.size();
        vector<int> a(m + 1);
        for (auto &x: flowers) {//差分数组实现"区间加"
            a[lower_bound(s.begin(), s.end(), x[0]) - s.begin()]++;
            a[lower_bound(s.begin(), s.end(), x[1]) - s.begin() + 1]--;
        }
        partial_sum(a.begin(), a.end(), a.begin());//ch
        vector<int> res;
        for (auto x: people)
            res.push_back(a[lower_bound(s.begin(), s.end(), x) - s.begin()]);
        return res;
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbNzA5MDQwMDAwLC0xNTAyNzE5NzUyLC0xMz
QzNTA2NTE1LC0yMDg4NzQ2NjEyLC0xNTAzNDEyMDI5LC04Mzc2
NTE3NDYsLTUyNzc5NTQ1NCwtODM4MDMzODkwLC0xOTIyOTYzMT
cwLDEyMzcyOTIxODUsMTc3NjAxMTEwMyw4MzMxODE4OTcsMTg1
NjgyODI5MV19
-->