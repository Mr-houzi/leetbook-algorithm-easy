# [191. 位1的个数](https://leetcode.cn/problems/number-of-1-bits/)

### 思路

利用十进制 1 (0000……001) 和 n 与运算，根据结果判断最低位的值。
- 若结果为 0 ，则最低位为 0；
- 若结果为 1 ，则最低位为 1；
将 n 右移后，继续与运算，然后判断。循环32次。

### 复杂度

时间复杂度：O(1)

空间复杂度：O(1)

### 代码

```php
class Solution {
    /**
     * @param Integer $n
     * @return Integer
     */
    function hammingWeight($n) {
        $counter = 0;
        $mask = 1;
        for($i = 0; $i < 32; $i++) {
            if(($n & $mask) == 1) {
                $counter++;
            }
            $n = $n >> 1;
        }

        return $counter;
    }
}
```