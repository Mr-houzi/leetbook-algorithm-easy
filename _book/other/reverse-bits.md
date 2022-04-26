# 颠倒二进制位

### 思路

逐位颠倒，用**1**与传入值进行**与运算**，可计算出最低位的值。

每次遍历时，
1. 传入值与 1 进行与运算，得出最低位的值；
2. 结果值 ans进行左移一位，然后加入最低位；
3. 传入值进行右移一位。

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
    function reverseBits($n) {
        $ans = 0;
        for($i = 0; $i < 32; $i++) {
            // 算出最低位的值
            $low = ($n & 1);
            // 将结果左移一位，然后加入最低位
            $ans = ($ans << 1) + $low ;
            $n = $n >> 1;
        }

        return $ans;
    }
}
```