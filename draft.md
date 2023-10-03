动态规划：设 $p[i][j]$ 为在 $prices[0,i-1]$ 中操作了 $j$ 次（买卖一只股票算两次）的最大收益，有

```cpp
class Solution {  
public:  
    int maxProfit(int k, vector<int> &prices) {  
        int n = prices.size();  
  int p[n + 1][k * 2 + 1];  
  for (int j = 1; j <= k * 2; j++)  
            p[0][j] = INT32_MIN;  
  p[0][0] = 0;  
  for (int i = 0; i < n; ++i) {  
            p[i + 1][0] = 0;  
  for (int j = 1; j <= k * 2; j++) {  
                p[i + 1][j] = INT32_MIN;  
  if (p[i][j] != INT32_MIN)  
                    p[i + 1][j] = max(p[i + 1][j], p[i][j]);  
  if (p[i][j - 1] != INT32_MIN)  
                    p[i + 1][j] = max(p[i + 1][j], p[i][j - 1] + (j & 1 ? -prices[i] : prices[i]));  
  }  
        }  
        int res = 0;  
  for (int j = 2; j <= 2 * k; j++)  
            if (p[n][j] != INT32_MIN)  
                res = max(res, p[n][j]);  
  return res;  
  }  
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTE0NjIwMTcxMiwtMjEyMTA1OTYyMywtMT
Y0Njg1MDQwLC0xNTAyNzE5NzUyLC0xMzQzNTA2NTE1LC0yMDg4
NzQ2NjEyLC0xNTAzNDEyMDI5LC04Mzc2NTE3NDYsLTUyNzc5NT
Q1NCwtODM4MDMzODkwLC0xOTIyOTYzMTcwLDEyMzcyOTIxODUs
MTc3NjAxMTEwMyw4MzMxODE4OTcsMTg1NjgyODI5MV19
-->