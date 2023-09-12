模拟：枚举可以攻击国王的 $8$ 个方向，每个方向遍历到边界外或第一个皇后为止。
```cpp
class Solution {
public:
    vector<vector<int>> queensAttacktheKing(vector<vector<int>> &queens, vector<int> &king) {
        int dr[8] = {-1, -1, -1, 0, 0, 1, 1, 1};
        int dc[8] = {-1, 0, 1, -1, 1, -1, 0, 1};
        int isq[8][8];//记录坐标是否有皇后
        memset(isq, 0, sizeof(isq));
        for (auto &qi: queens)
            isq[qi[0]][qi[1]] = 1;
        vector<vector<int>> res;
        for (int k = 0; k < 8; k++) {//枚举8个方向
            for (int nr = king[0] + dr[k], nc = king[1] + dc[k];; nr += dr[k], nc += dc[k]) {
                if (nr < 0 || nr >= 8 || nc < 0 || nc >= 8)//已出界
                    break;
                if (isq[nr][nc]) {//该方向的第一个皇后
                    res.push_back({nr, nc});
                    break;
                }
            }
        }
        return res;
    }
};
```


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE3NjgwNzQ5NzksLTgzNzY1MTc0NiwtNT
I3Nzk1NDU0LC04MzgwMzM4OTAsLTE5MjI5NjMxNzAsMTIzNzI5
MjE4NSwxNzc2MDExMTAzLDgzMzE4MTg5NywxODU2ODI4MjkxXX
0=
-->