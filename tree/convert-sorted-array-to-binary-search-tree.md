# [108. 将有序数组转换为二叉搜索树](https://leetcode.cn/problems/convert-sorted-array-to-binary-search-tree/)

### 思路

二分法（递归）

二叉搜索树是有序的，传入数组也是有序的，有序就要想到二分法。最简单保持树平衡的方式，就是使根节点左右子孙树节点相差不超过1个
（总节点数为奇数时，左右子树节点数相同；为偶数时，左右子树节点数差一）。

二叉搜索树中序遍历的结果，则是一个有序数组。但并不能确定根节点的位置，任何一个点都可能是根节点。当增加了**高度平衡**这个条件时，有序数组中间位置就可以确定是树的根节点了。以这个思路把有序数组重新构建回二叉搜索树。

### 复杂度

时间复杂度：O(nlogN)

php 内置函数 array_slice 为n，树构建为logN

空间复杂度：O(n)

递归栈为n

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
     * @param Integer[] $nums
     * @return TreeNode
     */
    function sortedArrayToBST($nums) {
        return $this->helper($nums, 0, count($nums) - 1);
    }

    function helper($nums, $low, $hight)
    {
        if($low > $hight) return null;

        $mid = intval(($low + $hight) / 2);

        $node = new TreeNode($nums[$mid]);
        $node->left = $this->helper($nums, $low, $mid - 1);
        $node->right = $this->helper($nums, $mid + 1, $hight);

        return $node;
    }
}
```