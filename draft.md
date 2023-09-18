状态规划：定义 $p[root,true]$ 为：以 $root$ 为的根子树能够得到的最高金额， $p[root,false]$ 为：以 $root$ 为的根子树不能打劫 $root$ 能够得到的最高金额，有状态转移方程 $\left\{\begin{matrix}
p[root][false]=p[root.left][true]+p[root.right][true] \\
p[root][true]=max\{p[root.left][true]+p[root.right][true],root.val+p[root.left][false]+p[root.right][false]\}
\end{matrix}\right.$

```cpp
class Solution {
public:
    int rob(TreeNode *root) {
        map<pair < TreeNode * , bool>, int > p;
        function<int(TreeNode *, bool)> dfs = [&](TreeNode *root, bool can) {
            if (!root)
                return 0;
            auto cur = make_pair(root, can);
            if (auto x = p.find(cur);x != p.end())//记忆化搜索避免重复计算
                return x->second;
            p[cur] = dfs(root->left, true) + dfs(root->right, true);
            if (can)
                p[cur] = max(p[cur], root->val + dfs(root->left, false) + dfs(root->right, false));
            return p[cur];
        };
        return dfs(root, true);
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM0MjYxMzQwLC0yMDg4NzQ2NjEyLC0xNT
AzNDEyMDI5LC04Mzc2NTE3NDYsLTUyNzc5NTQ1NCwtODM4MDMz
ODkwLC0xOTIyOTYzMTcwLDEyMzcyOTIxODUsMTc3NjAxMTEwMy
w4MzMxODE4OTcsMTg1NjgyODI5MV19
-->