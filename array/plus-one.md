# 加一

### 思路

加 1 操作会产生两种结果。

1. 非9 + 1 不产生进位；
2. 9 + 1 产生进位；特殊情况：各个位全为 9 ，加 1 后每个位都向前进 1，最终会导致这个数的位数增加。如：9999（4位数） + 1 = 10000 （5位数）

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```
class Solution {

    /**
     * @param Integer[] $digits
     * @return Integer[]
     */
    function plusOne($digits) {
        $len = count($digits);
        $i = $len -1;
        // 是否继续
        $flag = true;
        while($flag) {
            $sum = $digits[$i] + 1;
            if($sum > 9) {
                // 进位
                $flag = true;
                $digits[$i] = 0;
                
                // 当一直进位到最高位，需要增加一位
                if($i == 0) {
                    $digits = array_fill(0, $len + 1, 0);
                    $digits[0] = 1;
                    // 结束
                    break;
                }

                $i--;
            } else {
                // 不需要进位
                $digits[$i] = $sum;
                $flag = false;
            }
        }

        return $digits;
    }
}
```