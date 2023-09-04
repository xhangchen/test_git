前序遍历：将字符串序列化为前序遍历生成的字符串，非空节点在字符串中为其节点值，节点之间用`,`分割。因为是不含相同值的二叉搜索树，所以反序列化可以由前序遍历的结果递归地求树的结构。
```cpp
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode *root) {
        string res;
        function<void(TreeNode *)> dfs = [&](TreeNode *cur) {//先序遍历
            if (!cur)
                return;
            res.append(to_string(cur->val) + ",");
            dfs(cur->left);
            dfs(cur->right);
        };
        dfs(root);
        if (!res.empty())
            res.pop_back();
        return res;
    }

    // Decodes your encoded data to tree.
    TreeNode *deserialize(string data) {
        auto scan = [&data](int s, int e, int &val) {//扫描data[s]开头的数val,返回其最后数位的下标
            val = data[s] - '0';
            while (s + 1 <= e && isdigit(data[s + 1]))
                val = val * 10 + data[++s] - '0';
            return s;
        };

        function<TreeNode *(int, int)> get_root = [&](int s, int e) -> TreeNode * {
            if (s > e)
                return nullptr;
            int i, val_root;
            i = scan(s, e, val_root);
            TreeNode *root = new TreeNode(val_root);
            int j = i + 2, tmp;
            while (j <= e) {
                int last = scan(j, e, tmp);
                if (tmp < val_root)
                    j = last + 2;
                else {
                    root->left = get_root(i + 2, j - 2);//生成左子树
                    root->right = get_root(j, e);//生成右子树
                    return root;
                }
            }
            root->left = get_root(i + 2, e);//只有左子树的情况
            return root;
        };
        return get_root(0, data.size() - 1);
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTgzODAzMzg5MCwtMTkyMjk2MzE3MCwxMj
M3MjkyMTg1LDE3NzYwMTExMDMsODMzMTgxODk3LDE4NTY4Mjgy
OTFdfQ==
-->