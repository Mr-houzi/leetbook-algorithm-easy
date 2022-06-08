# [7. 整数反转](https://leetcode.cn/problems/reverse-integer/solution/)

### 思路

求一个整数各个位上的数：

一个数 mod(取模) 10，得到个位数；
将这个数除10 后，继续取模，可得到十位数；
如此循环，直到这个数为0时，便可得到各个位数的所有数。

以上过程，最先得出的一定是末位数（个位数），每次给取模的值乘10，加上原先的值，即可得到反转后的结果。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```
class Solution {

    /**
     * @param Integer $x
     * @return Integer
     */
    function reverse($x) {
        $value = 0;
        while($x != 0) {
            $mod = $x % 10;
            $x = intval($x / 10);
            $value = $value * 10 + $mod;
        }

        if($value > 2**31 -1 || $value < -2**31) $value = 0;

        return $value;
    }
}
```