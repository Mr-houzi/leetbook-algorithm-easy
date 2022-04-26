# 计数质数

### 思路

埃氏筛，某个数 i 的 j（j>1）倍一定是合数，标记出全部的合数，其余为质数。详细见代码。

### 复杂度

时间复杂度：O()

空间复杂度：O()

### 代码

```php
class Solution {

    /**
     * 埃氏筛
     * 某个数 i 的 j（j>1）倍一定是合数，标记出全部的合数，其余为质数
     * @param Integer $n
     * @return Integer
     */
    function countPrimes($n) {
        if($n <= 2) return 0;

        // 默认全为质数
        $hash = array_fill(2, $n - 2, 0);

        // 遍历将合数标记为1
        for($i = 2; $i < $n; $i++) {
            // 如果当前的数未被标记为合数，则判断遍历它的倍数将它的倍数标记为合数。
            // 如果当前的数已被标记为合数，那它的倍数一定也被标记为合数了，则跳过标记。
            if($hash[$i] == 0) {
                for($j = 2; $i * $j < $n; $j++) {
                    $hash[$i * $j] = 1;
                }
            }
        }

        return array_count_values($hash)[0];
    }
}
```