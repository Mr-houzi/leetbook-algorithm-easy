# [237. 删除链表中的节点](https://leetcode.cn/problems/delete-node-in-a-linked-list/)

### 思路

……

### 复杂度

时间复杂度：O(1)

空间复杂度：O(1)

### 代码

```
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val) { $this->val = $val; }
 * }
 */

class Solution {
    /**
     * @param ListNode $node
     * @return 
     */
    function deleteNode($node) {
        $node->val = $node->next->val;
        $node->next = $node->next->next;
    }
}
```