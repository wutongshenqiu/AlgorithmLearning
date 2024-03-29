- [二叉树](binary-tree.md)
  
  - 根据**中序 + 前序/后序**构建二叉树
  
  - 根据**前序+后序**构造二叉树
    
    - [PAT 1119](https://pintia.cn/problem-sets/994805342720868352/problems/994805353470869504)
  
  - 构建完全二叉搜索树
    
    - [PAT 1064](https://pintia.cn/problem-sets/994805342720868352/problems/994805407749357568)
  
  - 如何判断**完全二叉树**
    
    - 层次遍历中遍历到null之后没有其他节点
    - [PAT 1110](https://pintia.cn/problem-sets/994805342720868352/problems/994805359372255232)
  
  - 二叉树的**转置(inverted)**
    
    - 所有非叶子节点的左右子树互换
      
      - 也称为 `mirror of the input tree`
    
    - [PAT 1102](https://pintia.cn/problem-sets/994805342720868352/problems/994805365537882112)
    
    - [leetcode 剑指 Offer 28](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)
      
      - 如何判断二叉树是否是对称的(和镜像一样)？
        
        ```c++
        bool judge(TreeNode *left, TreeNode *right) {
            if (!left && !right) return true;
            if (left && right && left->val == right->val) {
                return judge(left->left, right->right) && 
                       judge(left->right, right->left);
            }
        
            return false;
        }
        ```
  
  - **栈**实现遍历
    
    - [PAT 1086](https://pintia.cn/problem-sets/994805342720868352/problems/994805380754817024)

- [红黑树](red-black-tree.md)
  
  - [PAT 1135](https://pintia.cn/problem-sets/994805342720868352/problems/994805346063728640)

- [平衡二叉树](avl-tree.md)
  
  - [PAT 1123](https://pintia.cn/problem-sets/994805342720868352/problems/994805351302414336)

- [树状数组](fenwick-tree.md)
  
  - [PAT 1057](https://pintia.cn/problem-sets/994805342720868352/problems/994805417945710592)

- [树的直径](tree-diameter.md)
  
  - [acwing 1207](https://www.acwing.com/problem/content/description/1209/)

- [树状数组](fenwick-tree.md)

- [线段树](segment-tree.md)