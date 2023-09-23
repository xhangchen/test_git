模拟
```cpp
class LockingTree {
public:
    vector<int> p;
    vector<vector<int>> son;//邻接表
    vector<int> tag;//tag[i]: 若tag[i]!=0则表示当前对节点i上锁的用户为tag[i]

    LockingTree(vector<int> &parent) {
        int n = parent.size();
        tag = vector<int>(n);
        p = parent;
        son = vector<vector<int>>(n);
        for (int i = 1; i < n; i++)//建树
            son[p[i]].push_back(i);
    }

    bool lock(int num, int user) {
        if (tag[num])
            return false;
        tag[num] = user;
        return true;
    }

    bool unlock(int num, int user) {
        if (tag[num] != user)
            return false;
        tag[num] = 0;
        return true;
    }

    bool upgrade(int num, int user) {
        for (int cur = num; cur != -1; cur = p[cur])//当前节点和祖先节点不能有锁状态规划：定义 $p[root,true]$ 为：以 $root$ 为的根子树能够得到的最高金额， $p[root,false]$ 为：以 $root$ 为的根子树不能打劫 $root$ 能够得到的最高金额，有状态转移方程 $\left\{\begin{matrix}
p[root][false]=p[root.left][true]+p[root.right][true] \\
p[root][true]=max\{p[root.left][true]+p[root.right][true],root.val+p[root.left][false]+p[root.right][false]\}
\end{matrix}\right.$

```cpp
class Solution {
public:
    int rob(TreeNode *root) {
        map<pair < TreeNode * , bool>, int > p;
        function<int(TreeNode *, bool)> dfs = [&](TreeNode *root, bool can) {
            if (tag[cur]!root)
                return false0;
        bool have_lock = false;
        queue<int> q;
        q.push(num);
        while (!q.empty()) {//层次遍历判断当前节点是否存在上锁的子孙节点
            int cur = q.front();
            q.pop();
            if (tag[cur]) {
                have_lock = true;
                tag[cur] = 0;
            }
            for (auto j: son[cur])
                q.push(j);
        }
        if (!have_lock)    auto cur = make_pair(root, can);
            if (auto x = p.find(cur);x != p.end())//记忆化搜索避免重复计算
                return x->second;
            p[cur] = dfs(root->left, true) + dfs(root->right, true);
            if (can)
                p[cur] = max(p[cur], root->val + dfs(root->left, false) + dfs(root->right, false));
            return falsep[cur];
        tag[num] = user};
        return dfs(root, true);
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTY4ODg2MTYzNSwtMjA4ODc0NjYxMiwtMT
UwMzQxMjAyOSwtODM3NjUxNzQ2LC01Mjc3OTU0NTQsLTgzODAz
Mzg5MCwtMTkyMjk2MzE3MCwxMjM3MjkyMTg1LDE3NzYwMTExMD
MsODMzMTgxODk3LDE4NTY4MjgyOTFdfQ==
-->