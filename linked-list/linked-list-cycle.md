# [141. 环形链表](https://leetcode.cn/problems/linked-list-cycle/)

### 思路

快慢指针法:

- 快指针在前，每次走2步
- 慢指针在后，每次走1步

判定有环：当快指针遇上慢指针则为有环

**为什么快指针每次走2步？**

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

# 系列题

## [142. 环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/)

### 思路

判断环形链表入口
1. 利用快慢指针判断是否存在环，快指针走两步，慢指针走一步，两者若能相遇，则存在环;
2. 快慢指针相遇后，快指针改为走一步；另取一辅助指针，从头开始也是每次走一步；两者相遇的节点，便是环形链表入口。

**为什么快指针和辅助指针相遇，则为环形链表入口？**

见官方题解[环形链表 II](https://leetcode.cn/problems/linked-list-cycle-ii/solution/huan-xing-lian-biao-ii-by-leetcode-solution/)方法二的数学推论；

![](https://assets.leetcode-cn.com/solution-static/142/142_fig1.png)

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```golang
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func detectCycle(head *ListNode) *ListNode {
	fast, low, p := head, head, head
	
    // 利用相遇判断环
    for {
		// 若不存在环，返回nil
		if fast == nil || fast.Next == nil {
			return nil
		}

		// 移动
		fast = fast.Next.Next
		low = low.Next

		// 相遇
		if fast == low {
			break
		}
	}

    // 相遇后，fast 改为每次走一步； p 从链表开头每次走一步；两者相遇的节点，则是环形链表入口；
	for p != fast {
		p = p.Next
		fast = fast.Next
	}

	return p
}
```