动态规划：设$m$，$n$为矩阵行数和列数，定义状态$p_{row,col,mask}$为当前位置为$(row,col)$，且当前经过的位置的状态为$mask$(mask 二进制表示中第$r\times n+c$位为1，当且仅当已经经过位置$(r,c)$)的情况下能够到达结束方格并经过所有无障碍方格的路径数。通过回溯+记忆化搜索来枚举所有可能到达的状态。

```cpp
class Solution {  
public:  
    int uniquePathsIII(vector<vector<int>> &grid) {  
        int m = grid.size(), n = grid[0].size(), N = 1 << (m * n);  
        int mask0 = 0;  //初始状态  
  auto id = [&](int &r, int &c) { return r * n + c; };  //把二维坐标映射到一维  
  int sr, sc;  //初始坐标  
  for (int i = 0; i < m; i++)  
            for (int j = 0; j < n; j++)  
                if (grid[i][j] == -1)  
                    mask0 |= 1 << id(i, j); //不能到达的位置  
  else if (grid[i][j] == 1) {  
                    mask0 |= 1 << id(i, j);  
                    sr = i;  
                    sc = j;  
                }  
        int p[m][n][N];  
        memset(p, -1, sizeof(p));  
        int dr[4] = {1, -1, 0, 0}, dc[4] = {0, 0, 1, -1};  
        function<int(int, int, int)> dfs = [&](int row, int col, int mask) {//记忆化搜索  
  if (p[row][col][mask] != -1)  
                return p[row][col][mask];  
            int &cur = p[row][col][mask];  
            if (grid[row][col] == 2)  //到达结束方格，判断是否所有无障碍方格  
  return cur = (mask == N - 1 ? 1 : 0);  
            cur = 0;  
            for (int k = 0; k < 4; k++) {  
                int nr = row + dr[k];  
                int nc = col + dc[k];  
                if (nr < 0 || nr >= m || nc < 0 || nc >= n || mask >> id(nr, nc) & 1) //不能前往已经经过或障碍位置 
                    continue;  
                cur += dfs(nr, nc, mask | 1 << id(nr, nc));  
            }  
            return cur;  
        };  
        return dfs(sr, sc, mask0);  
    }  
};
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg1NjgyODI5MV19
-->