
$bfs$：

```cpp

class Codec {
public:
    string ch_null = "null";

    // Encodes a tree to a single string.
    string serialize(TreeNode *root) {
        string res;
        queue<TreeNode *> q;
        q.push(root);
        res.push_back('[');
        while (!q.empty()) {
            auto cur = q.front();
            q.pop();
            if (cur) {
                res.append(to_string(cur->val) + ",");
                q.push(cur->left);
                q.push(cur->right);
            } else
                res.append(ch_null + ",");
        }
        int tail = res.size() - 1;
        while (tail - 1 >= 0 && res[tail - 1] == ch_null.back())
            tail -= 5;
        res = res.substr(0, tail + 1);
        res.back() = ']';
        return res;
    }

    // Decodes your encoded data to tree.
    TreeNode *deserialize(string data) {
        if (data.size() == 2)
            return nullptr;
        TreeNode *root = nullptr;
        reference_wrapper<TreeNode *> cur = root;
        queue<reference_wrapper<TreeNode *>> q;
        q.push(cur);
        int i = 1;
        while (i < data.size() && !q.empty()) {
            auto cur = q.front();
            q.pop();
            if (data[i] == ch_null[0]) {
                i += 5;
            } else {
                int j = i;
                while (isdigit(data[j + 1]))
                    j++;
                cur.get() = new TreeNode(stoi(data.substr(i, j - i + 1)));
                q.push(ref(cur.get()->left));
                q.push(ref(cur.get()->right));
                i = j + 2;
            }
        }
        return root;
    }
};
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTIyNDU0NzIyNCwxMjM3MjkyMTg1LDE3Nz
YwMTExMDMsODMzMTgxODk3LDE4NTY4MjgyOTFdfQ==
-->