模拟
```cpp
class Solution {
public:
    vector<int> filterRestaurants(vector<vector<int>> &restaurants, int veganFriendly, int maxPrice, int maxDistance) {
        vector<int> ind(restaurants.size());
        iota(ind.begin(), ind.end(), 0);//ind: 0,1,...
        auto x = partition(ind.begin(), ind.end(), [&](int i) { return restaurants[i][2] >= veganFriendly && restaurants[i][3] <= maxPrice && restaurants[i][4] <= maxDistance; });//将不被过滤的元素移至数组前面
        ind.erase(x, ind.end());//将数组后面的过滤元素删除
        sort(ind.begin(), ind.end(), [&](int x, int y) {//排序
            if (restaurants[x][1] != restaurants[y][1])
                return restaurants[x][1] > restaurants[y][1];
            return restaurants[x][0] > restaurants[y][0];
        });
        vector<int> res;
        transform(ind.begin(), ind.end(), back_inserter(res), [&](int x) { return restaurants[x][0]; });//生成id数组
        return res;
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzNDM1MDY1MTUsLTIwODg3NDY2MTIsLT
E1MDM0MTIwMjksLTgzNzY1MTc0NiwtNTI3Nzk1NDU0LC04Mzgw
MzM4OTAsLTE5MjI5NjMxNzAsMTIzNzI5MjE4NSwxNzc2MDExMT
AzLDgzMzE4MTg5NywxODU2ODI4MjkxXX0=
-->