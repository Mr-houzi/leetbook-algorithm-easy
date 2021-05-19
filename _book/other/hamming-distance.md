# 汉明距离

### 思路

让 x，y 两数进行异或（同为0，异为1）运算，结果值二进制中 1 的个数，就代表两数字对应二进制位不同的位置的个数。

在利用 [题：位1的个数](./number-of-1-bits.md) 来计算二进制数中 1 的个数。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```php
class Solution {

    /**
     * @param Integer $x
     * @param Integer $y
     * @return Integer
     */
    function hammingDistance($x, $y) {
        $z = $x ^ $y; // 异或

        return $this->hammingWeight($z);
    }

    /**
     * 题：位1的个数
     */
    function hammingWeight($num) {
        $counter = 0;
        $mask = 1;
        while($num > 0) {
            if($num & $mask == 1) {
                $counter++;
            }
            $num = $num >> 1;
        }

        return $counter;
    }
}
```