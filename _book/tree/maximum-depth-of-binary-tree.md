# 二叉树的最大深度

## 方法一、深度优先搜索

### 思路

深度优先搜索

递归法

1. 左子树和右子树的最大深度 ll 和 rr，那么该二叉树的最大深度即为 max(l,r) + 1
2. 当前节点为 null 时， 深度为 0（递归的终止条件）

### 复杂度

时间复杂度：O(n)

空间复杂度：O(h)

递归最大深度为h

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
     * @return Integer
     */
    function maxDepth($root) {
        if($root === null) return 0;

        return max($this->maxDepth($root->left), $this->maxDepth($root->right)) + 1;
    }
}
```

## 方法二、广度优先搜索

### 思路

基于广度优先搜索（非递归法）的变形。

广度优先搜索是每次从队列中取出一个节点进行消费，并把它的左右节点（若存在）放入队尾。
变形后，让每次消费节点时，遍历（内层）取出队列中当前层全部的节点，并把它的左右节点（若存在）放入队尾，这样用计数器记录外层遍历的次数，即最大高度。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(m)

队列大小m，最坏为n

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
     * @return Integer
     */
    function maxDepth($root) {
        if(!$root) return 0;
        $list = [];
        $list[] = $root;
        $height  = 0;
        while(count($list) > 0) {
            $curlen = count($list);
            // 每次取出当前层全部的节点
            while( $curlen > 0 ) {
                $top = array_shift($list);
                if($top->left) $list[] = $top->left;
                if($top->right) $list[] = $top->right;
                $curlen--;
            }
            $height++;
        }

        return $height;
    }
}
```