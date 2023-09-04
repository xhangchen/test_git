层次遍历：将字符串序列化为层次遍历生成的字符串，非空节点在字符串中为其节点值，空节点为字符串`null`，节点之间用`,`分割，遍历完后去掉末尾连续的`null`。反序列的过程类似，实现可以用 `reference_wrapper` 将指针的 “引用” 放入队列，之后再对其赋值。

```cpp

class Codec {
public:
    string ch_null = "null";//空指针标志

    string serialize(TreeNode *root) {
        string res;
        queue<TreeNode *> q;
        q.push(root);
        res.push_back('[');//字符串开头
        while (!q.empty()) {//层次遍历
            auto cur = q.front();
            q.pop();
            if (cur) {//非空节点
                res.append(to_string(cur->val) + ",");
                q.push(cur->left);
                q.push(cur->right);
            } else
                res.append(ch_null + ",");
        }
        int tail = res.size() - 1;
        while (tail - 1 >= 0 && res[tail - 1] == ch_null.back())//去掉末尾连续的 null
            tail -= 5;
        res = res.substr(0, tail + 1);
        res.back() = ']';//字符串结尾
        return res;
    }

    TreeNode *deserialize(string data) {
        if (data.size() == 2)//空树
            return nullptr;
        TreeNode *root = nullptr;
        reference_wrapper<TreeNode *> cur = root;
        queue<reference_wrapper<TreeNode *>> q;// 存放指针的“引用”
        q.push(cur);
        int i = 1;
        while (i < data.size() && !q.empty()) {//层次遍历
            auto cur = q.front();
            q.pop();
            if (data[i] == ch_null[0]) {//空节点
                i += 5;
            } else {
                int j = i;
                while (isdigit(data[j + 1]))
                    j++;
                cur.get() = new TreeNode(stoi(data.substr(i, j - i + 1)));//当前位置创建节点
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
eyJoaXN0b3J5IjpbLTE5MjI5NjMxNzAsMTIzNzI5MjE4NSwxNz
c2MDExMTAzLDgzMzE4MTg5NywxODU2ODI4MjkxXX0=
-->