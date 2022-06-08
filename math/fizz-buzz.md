# [412. Fizz Buzz](https://leetcode.cn/problems/fizz-buzz/)

### 思路

没难度，直接按题意来。

关于 FizzBuzz 问题还有一个不错的小文章[我倒要看看一个FizzBuzz能讲多少道理](https://zhuanlan.zhihu.com/p/151740475)

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```php
class Solution {

    /**
     * @param Integer $n
     * @return String[]
     */
    function fizzBuzz($n) {
        $output = [];
        for($i = 1; $i <= $n; $i++) {
            $str = '';
            if($i % 3 == 0) $str .= 'Fizz';
            if($i % 5 == 0) $str .= 'Buzz';

            if($i % 3 != 0 && $i % 5 != 0) $str .= $i;

            $output[] = $str;
        }

        return $output;
    }
}
```