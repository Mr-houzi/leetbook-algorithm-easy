# 最小栈

### 思路

利用一个数组模拟栈，一个数组存储当前栈的最小值。

### 复杂度

时间复杂度：O()

空间复杂度：O()

### 代码

```php
class MinStack {

    // 栈
    private $stack = [];
    // 最小值辅助栈
    private $minStack = [];

    /**
     * initialize your data structure here.
     */
    function __construct() {

    }

    /**
     * @param Integer $val
     * @return NULL
     */
    function push($val) {
        $this->stack[] = $val;
        if(count($this->minStack) == 0) {
            $this->minStack[] = $val;
        } else {
            $this->minStack[] = min($this->minStack[count($this->minStack) - 1], $val);
        }
    }

    /**
     * @return NULL
     */
    function pop() {
        if(count($this->stack)) {
            array_pop($this->stack);
            array_pop($this->minStack);
        }
    }

    /**
     * @return Integer
     */
    function top() {
        if(count($this->stack)) {
            return $this->stack[count($this->stack) - 1];
        }
    }

    /**
     * @return Integer
     */
    function getMin() {
        if(count($this->stack)) {
            return $this->minStack[count($this->minStack) - 1];
        }
    }
}
```