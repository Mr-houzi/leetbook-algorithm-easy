# 环形链表

### 思路

快慢指针法
快指针在前，每次走2步
慢指针在后，每次走1步
判定有环：当快指针遇上慢指针则为有环
为什么快指针每次走2步？
原因：具体走几步可以自己设定，让快指针每次走2步，而慢指针每次走1步，这样的话，误差较小，快指针在一圈就有可能遇上（位置重合）慢指针。
如果步长过大，可能要多圈才能完成两指针的遇上（位置重合）。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```php
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
     * @param ListNode $head
     * @return Boolean
     */
    function hasCycle($head) {
        $p1 = $head;
        $p2 = $head;

        while($p1->next != null && $p2->next != null) {
            $p1 = $p1->next;
            $p2 = $p2->next->next;
            if($p1 == $p2) {
                return true;
            }
        }

        return false;
    }
}
```