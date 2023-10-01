
### A [收集元素的最少操作次数](https://leetcode.cn/problems/minimum-operations-to-collect-elements/)

> 模拟: 反序遍历数组，用一个集合存当前遍历过的不超过 $k$ 的正数
```cpp
class Solution {
public:
    int minOperations(vector<int> &nums, int k) {
        unordered_set<int> vis;
        int n = nums.size();
        int i = n - 1;
        for (;; i--) {
            if (nums[i] <= k && !vis.count(nums[i]))
                vis.insert(nums[i]);
            if (vis.size() == k)
                break;
        }
        return n - i;
    }
};
```
___

### B [使数组为空的最少操作次数](https://leetcode.cn/problems/minimum-number-of-operations-to-make-array-empty/)

>计数：记录数组中各元素出现次数，若存在只出现一次的元素则无法使数组为空，否则，要将出现次数为 $f$ 的某个元素全部删除最少需要的次数为：当 $f\%3=0$ 时为 $\frac f 3$ ，当 $f\%3\ne 0$ 时为 $\left \lfloor \frac f 3 \right \rfloor + 1$ 。

```cpp
class Solution {
public:
    int minOperations(vector<int> &nums) {
        unordered_map<int, int> cnt;
        for (auto x: nums)
            cnt[x]++;
        int res = 0;
        for (auto [_, f]: cnt) {
            if (f == 1)
                return -1;
            if (f % 3 == 0)
                res += f / 3;
            else
                res += f / 3 + 1;
        }
        return res;
    }
};
```
___

### C [将数组分割成最多数目的子数组](https://leetcode.cn/problems/split-array-into-maximum-number-of-subarrays/)

>模拟：遍历数组元素 $nums[i]$ ，若 $nums[i]$ 不是最后一个元素，则只有一种情况会使得最优解中 $nums[i]$ 为其所在子数组的最后一个元素：$nums[i]$ 所在的子数组分数已经为 $0$ 且 $nums[i+1]\&\cdots\&nums[nums.size()-1]$ 等于 $0$

```cpp
class Solution {
public:
    int maxSubarrays(vector<int> &nums) {
        int n = nums.size();
        vector<int> sf(n);//“后缀与”数组
        sf[n - 1] = nums[n - 1];
        for (int i = n - 2; i >= 0; i--)
            sf[i] = nums[i] & sf[i + 1];
        int res = 0;
        for (int i = 0, cur = nums[0]; i < n; i++) {
            cur &= nums[i];
            if (i == n - 1 || cur == 0 && sf[i + 1] == 0) {//nums[i]为所在子数组的最后一个元素
                res++;
                if (i != n - 1)
                    cur = nums[i + 1];//下一个子数组的首个元素
            }
        }
        return res;
    }
};
```
___

### D [可以被 K 整除连通块的最大数目](https://leetcode.cn/problems/maximum-number-of-k-divisible-components/)

> $dfs$：不妨以 $0$ 为树根，通过 $dfs$ 求 $s$ 数组： $s[i]$ 为以  $i$ 为根的子树的所有节点值之和。设 $dfs$ 遍历到的当前节点为 $cur$ ，若遍历到 $cur$ 的子节点 $j$ 时，有 $s[j]\%k==0$ ，则边 $(cur,j)$ 可以删除（即可以增加一个连通块）。


```cpp
class Solution {
public:
    using ll = long long;

    int maxKDivisibleComponents(int n, vector<vector<int>> &edges, vector<int> &values, int k) {
        vector<int> e[n];//邻接表
        for (auto &ei: edges) {//建图
            e[ei[0]].push_back(ei[1]);
            e[ei[1]].push_back(ei[0]);
        }
        vector<ll> s(n);
        int res = 1;
        function<ll(int, int)> dfs = [&](int cur, int par) {//当前节点为cur,父节点为par
            s[cur] += values[cur];
            for (auto j: e[cur])
                if (j != par) {
                    s[cur] += dfs(j, cur);
                    if (s[j] % k == 0)
                        res++;
                }
            return s[cur];
        };
        dfs(0, -1);//以0为根跑dfs
        return res;
    }
};
```

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIxMjEwNTk2MjMsLTE2NDY4NTA0MCwtMT
UwMjcxOTc1MiwtMTM0MzUwNjUxNSwtMjA4ODc0NjYxMiwtMTUw
MzQxMjAyOSwtODM3NjUxNzQ2LC01Mjc3OTU0NTQsLTgzODAzMz
g5MCwtMTkyMjk2MzE3MCwxMjM3MjkyMTg1LDE3NzYwMTExMDMs
ODMzMTgxODk3LDE4NTY4MjgyOTFdfQ==
-->