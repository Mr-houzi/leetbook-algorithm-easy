# 二叉树的层序遍历

## 方法一

### 思路

为了在输出中体现出“层”的概念，每次从队列中取出当前层的所有节点。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(n)

### 代码

```php
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($val = 0, $left = null, $right = null) {
 *         $this->val = $val;
 *         $this->left = $left;
 *         $this->right = $right;
 *     }
 * }
 */
class Solution {

    /**
     * @param TreeNode $root
     * @return Integer[][]
     */
    function levelOrder($root) {

        if($root == null) return [];

        // 队列
        $list = [];
        $list[] = $root;

        // 结果集
        $output = [];
        while(count($list) > 0) {
            $curlen = count($list);
            $temp = [];
            // 取出当前层的所有节点
            while($curlen > 0) {
                $top = array_shift($list);
                $temp[] = $top->val;
                if($top->left) $list[] = $top->left;
                if($top->right) $list[] = $top->right;
                $curlen--;
            }

            $output[] = $temp;
        }

        return $output;
    }
}
```

## 方法二

### 思路

由于输出时，需要体现“层”，队列的每个 item 需要保存**节点**和**节点的层数**。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(n)

### 代码

```php
/**
 * Definition for a binary tree node.
 * class TreeNode {
 *     public $val = null;
 *     public $left = null;
 *     public $right = null;
 *     function __construct($value) { $this->val = $value; }
 * }
 */
class Solution {

    /**
     * @param TreeNode $root
     * @return Integer[][]
     */
    function levelOrder($root) {
        if($root === null) return [];

        // 队列
        $list = [
            [$root, 1], // 根节点
        ];
        // 输出
        $output = [[$root->val]];
        while(count($list) > 0) {
            list($node, $level) = array_shift($list);
            if($node->left !== null) {
                $output[$level][] = $node->left->val;
                $list[] = [$node->left, $level + 1];
            }
            if($node->right !== null) {
                $output[$level][] = $node->right->val;
                $list[] = [$node->right, $level + 1];
            }
        }

        return $output;
    }
}
```