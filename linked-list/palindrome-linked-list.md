# [234. 回文链表](https://leetcode.cn/problems/palindrome-linked-list/)

### 思路

1. 获取链表长度
2. 将链表一分为二
3. 反转其中一个链表进行比较

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
    function isPalindrome($head) {
        $p = $head;
        
        // 长度
        $len = 0;
        while($p != null) {
            $len++;
            $p = $p->next;
        }

        // 第二段链表的起始位置
        $start = (int)(($len + 1)/2) + 1;

        $p = $head;
        $counter = 1;
        while($counter < $start) {
            $counter++;
            if($counter == $start){
                // 拆链
                $tmp = $p->next;
                $p->next = null;
                $p = $tmp;
            } else {
                $p = $p->next;
            }
        }

        // 反转第二段链表
        $p = $this->reverseList($p);
        while($p->val !== null) {
            if($p->val !== $head->val){
                return false;
            }
            $head = $head->next;
            $p = $p->next;
        }

        return true;
    }

    /**
     * 反转链表
     * @param ListNode $head
     * @return ListNode
     */
    function reverseList($head) {
        $p = null;

        while($head != null) {
            $tmp = $head;
            $head = $head->next;
            $tmp->next = $p;
            $p = $tmp;
        }

        return $p;
    }
}
```