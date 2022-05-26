# 爬楼梯

### 思路

动态规划

第1级台阶：1种方法（爬1级）；
第2级台阶：2种方法（爬2个1级或1个2级）；
第N级台阶：从第n-1级台阶爬1级或从第n-2级台阶爬2级（由于限制只能爬1级或2级）；
所以第N级台阶的爬楼方案等于n-1级方案和n-2级方案之和，即f(n) = f(n-1) + f(n-2)。

推出动态方程公式后，很容易想到递归法，但是递归法，重复计算量大，运行时间超时。所以使用三个滑动块来做，方案更优。

```
// 递归
function helper($n){
    if($n == 1) return 1;
    if($n == 2) return 2;

    // 这次多次重复递归计算
    return $this->helper($n - 1) + $this->helper($n - 2);
}
```

这题也符合斐波那契数列。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

php

```php
class Solution {

    /**
     * @param Integer $n
     * @return Integer
     */
    function climbStairs($n) {
        $p1 = 0;
        $p2 = 0;
        $p3 = 1; // 第一个点 i = 1 的值
        for($i = 1; $i <= $n; $i++) {
            // 向前滑动
            $p1 = $p2;
            $p2 = $p3;
            // 计算新进入滑动区间的块
            $p3 = $p1 + $p2;
        }

        return $p3;
    }
}
```

golang

```golang
// dp方程：f(n) = f(n-1) + f(n-2)
func climbStairs(n int) int {
	p1 := 0
	p2 := 0
	p3 := 1
	for i := 1; i <= n; i++ {
		p1 = p2
		p2 = p3
		
		p3 = p1 + p2
	}
	
	return p3
}
```