# 有效的括号

### 思路

利用栈来做。

1. 当字符为 '(', '{', '['时入栈；
2. 当字符为 ')', '}', ']'时，栈不为空，出栈并判断栈顶元素是否与当前符合对应；
3. 遍历结束后，栈要为空，才证明字符串中括号正确。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(m)

### 代码

```php
class Solution {

    /**
     * @param String $s
     * @return Boolean
     */
    function isValid($s) {
        $stack = [];

        for($i = 0; $i < strlen($s); $i++) {
            if(in_array($s[$i], ['(', '{', '['])) {
                // 入栈
                $stack[] = $s[$i];
            } else {
                // 出栈
                if(count($stack) === 0 ) return false;
                $top = array_pop($stack);
                if($top == '(' && $s[$i] != ')') return false;
                if($top == '{' && $s[$i] != '}') return false;
                if($top == '[' && $s[$i] != ']') return false;
            }
        }

        // 栈要为空
        if(count($stack) !== 0 ) return false;

        return true;
    }
}
```