# 反转链表

## 方法一、遍历法

### 思路

利用一个辅助指针 p 和一个临时指针 tmp 维护一个新链表。一边遍历，一边把指针指向掉头，指向新链表。

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
 *     function __construct($val = 0, $next = null) {
 *         $this->val = $val;
 *         $this->next = $next;
 *     }
 * }
 */
class Solution {

    /**
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

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func reverseList(head *ListNode) *ListNode {
	var pre *ListNode
	for head != nil {
		temp := head
		head = head.Next
		temp.Next = pre
		pre = temp
	}
	
	return pre
}
```

## 方法二、递归法

### 思路

终止条件：节点为空或节点的指向为空
“递”：指针后移一步
“归”：局部反转指针

关键是利用指针 p 和 head ，使指针 p 一直指向反转前的链表尾部，方便直接返回。
head 指向递归时的当前节点，利用 `$head->next->next = $head` 和 `$head->next = null` 进行局部节点指向掉头；
每次都返回始终指向反转前的链表尾部（也即反转后链表的头）的指针p。

PS： 指针 p 和 head 始终操作的是同一条链表。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(n)

递归法会产生为 n 的调用栈。

### 代码

```php
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
     * @return ListNode
     */
    function reverseList($head) {
        return $this->helper($head);
    }

    function helper($head){
        if($head == null || $head->next == null) return $head;

        $p = $this->helper($head->next);
        $head->next->next = $head;
        $head->next = null;
        return $p;
    }
}
```