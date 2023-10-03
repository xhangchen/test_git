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
eyJoaXN0b3J5IjpbNjgyMDg1NTg0LC0yMTIxMDU5NjIzLC0xNj
Q2ODUwNDAsLTE1MDI3MTk3NTIsLTEzNDM1MDY1MTUsLTIwODg3
NDY2MTIsLTE1MDM0MTIwMjksLTgzNzY1MTc0NiwtNTI3Nzk1ND
U0LC04MzgwMzM4OTAsLTE5MjI5NjMxNzAsMTIzNzI5MjE4NSwx
Nzc2MDExMTAzLDgzMzE4MTg5NywxODU2ODI4MjkxXX0=
-->