# [155. 最小栈](https://leetcode.cn/problems/min-stack/)

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

```golang
type MinStack struct {
	min []int
	stack []int
}


func Constructor() MinStack {
	return MinStack{}
}


func (this *MinStack) Push(val int)  {
	this.stack = append(this.stack, val)
	if len(this.min) == 0 {
		this.min = append(this.min, val)
	} else {
		if this.min[len(this.min)-1] > val {
			this.min = append(this.min, val)
		} else {
			this.min = append(this.min, this.min[len(this.min)-1])
		}
	}
}


func (this *MinStack) Pop()  {
	this.stack = this.stack[:len(this.stack)-1]
	this.min = this.min[:len(this.min)-1]
}


func (this *MinStack) Top() int {
	return this.stack[len(this.stack)-1]
}


func (this *MinStack) GetMin() int {
	return this.min[len(this.min)-1]
}

/**
 * Your MinStack object will be instantiated and called as such:
 * obj := Constructor();
 * obj.Push(val);
 * obj.Pop();
 * param_3 := obj.Top();
 * param_4 := obj.GetMin();
 */
```