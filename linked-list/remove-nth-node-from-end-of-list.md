# [19. 删除链表的倒数第 N 个结点](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)

### 思路

快慢指针法，利用指针p1、p2，让p1先走n步；然后p1、p2一起走，直到p1走到最后一个节点，p2这是恰巧走到倒数n+1个节点，然后进行删除操作。

处理特殊情况：若p1走完n步，p1为空，则证明删除的是第一个节点。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```
/**
 * Definition for a singly-linked list.
 * class ListNode {
 *     public $val = 0;
 *     public $next = null;
 *     function __construct($val = 0, $next = null) {
 *         $this->val = $val;
 *         $this->next = $next;
 *     }
 * }
 */
class Solution {

    /**
     * @param ListNode $head
     * @param Integer $n
     * @return ListNode
     */
    function removeNthFromEnd($head, $n) {
        $p1 = $head;
        $p2 = $head;
        // p1 先走n步
        for($i = 0; $i < $n; $i++){
            $p1 = $p1->next;
        }

        // p1 为空证明是删除的第一个是节点
        if($p1 == null) return $head->next;

        while($p1->next != NULL) {
            $p1 = $p1->next;
            $p2 = $p2->next;
        }

        $q = $p2->next;
        $p2->next = $p2->next->next;
        unset($q);

        return $head;
    }
}
```