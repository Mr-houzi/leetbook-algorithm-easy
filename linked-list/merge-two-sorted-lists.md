# [21. 合并两个有序链表](https://leetcode.cn/problems/merge-two-sorted-lists/)

### 思路

三指针遍历，利用两个指针遍历分别遍历两个链表，并比较对应值的大小，新指针指向小的节点，小的一方的指针也要往后移。

最后，要处理一下[一个长链，一个短链，长链还没走完]的情况。

### 复杂度

时间复杂度：O(m)

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
     * @param ListNode $l1
     * @param ListNode $l2
     * @return ListNode
     */
    function mergeTwoLists($l1, $l2) {
        $list = new ListNode(-1);
        $p = $list;
        // 只有一个链遍历完，则退出
        while($l1 != null && $l2 != null){

            if($l1->val <= $l2->val){
                $p->next = $l1;
                $l1 = $l1->next;
            } else {
                $p->next = $l2;
                $l2 = $l2->next;
            }

            $p = $p->next;
        }

        // 若一个长链，一个短链，长链还没走完
        $p->next = $l1 === null ? $l2 : $l1;

        // 去除头节点
        return $list->next;
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
func mergeTwoLists(list1 *ListNode, list2 *ListNode) *ListNode {
	list := &ListNode{
		Val:  0,
		Next: nil,
	}
	p := list

	for list1 != nil && list2 != nil {
		if list1.Val <= list2.Val {
			p.Next = list1
			list1 = list1.Next
		} else {
			p.Next = list2
			list2 = list2.Next
		}

		p = p.Next
	}

	if list1 == nil {
		p.Next = list2
	}

	if list2 == nil {
		p.Next = list1
	}

	return list.Next
}
```