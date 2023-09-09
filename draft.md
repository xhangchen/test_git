排序：若棋盘左上角不为 $0$ 直接返回 $false$，将坐标按坐标上的值的大小升序排序，设相邻坐标的横纵坐标绝对值为 $dx$ 和 $dy$，相邻坐标可以通过一次移动相互到达当且仅当 $min(dx,dy)=1$ 且 $max(dx,dy)=2$，遍历相邻坐标进行判断。
```cpp
class Solution {
public:
    bool checkValidGrid(vector<vector<int>> &grid) {
        if (grid[0][0] != 0)
            return false;
        int n = grid.size();
        vector<pair<int, int>> li(n * n);
        for (int i = 0; i < n; i++)
            for (int j = 0; j < n; j++)
                li[i * n + j] = {i, j};
        sort(li.begin(), li.end(), [&](pair<int, int> &a, pair<int, int> &b) { return grid[a.first][a.second] < grid[b.first][b.second]; });
        for (int i = 1; i < n * n; i++) {
            int dx = abs(li[i].first - li[i - 1].first);
            int dy = abs(li[i].second - li[i - 1].second);
            if (min(dx, dy) != 1 || max(dx, dy) != 2)
                return false;
        }
        return true;
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM1MjQ1NDA4NywtODM4MDMzODkwLC0xOT
IyOTYzMTcwLDEyMzcyOTIxODUsMTc3NjAxMTEwMyw4MzMxODE4
OTcsMTg1NjgyODI5MV19
-->