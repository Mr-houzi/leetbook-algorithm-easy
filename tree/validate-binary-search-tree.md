# 验证二叉搜索树

### 思路

二叉搜索树特征
1.节点的左子树只包含小于当前节点的数。
2.节点的右子树只包含大于当前节点的数。
3.所有左子树和右子树自身必须也是二叉搜索树。

递归法

判断当前节点是否符合二叉搜索树
终止：当前为空；
递：所有左子树和右子树自身必须“先是”二叉搜索树；
归：判断节点值是否在 (min, max) 范围内。


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
     * @return Boolean
     */
    function isValidBST($root) {
        return $this->helper($root, '-inf', '+inf');
    }

    /**
     * 判断当前节点是否符合二叉搜索树
     * @param min 表示当前节点的最小取值（开区间点），-inf 表示负无穷
     * @param max 表示当前节点的最大取值（开区间点），+inf 表示正无穷
     */
    function helper($root, $min, $max)
    {
        if($root === null) return true;

        // 所有左子树和右子树自身必须“先是”二叉搜索树。
        if(!$this->helper($root->left, $min, $root->val)){
            return false;
        }

        if(!$this->helper($root->right, $root->val, $max)){
            return false;
        }

        // 判断节点值是否在 (min, max) 范围内
        if( $min !== '-inf' && $root->val <= $min )  {
            return false;
        }

        if( $max !== '+inf' && $root->val >= $max )  {
            return false;
        }

        return true;
    }
}
```