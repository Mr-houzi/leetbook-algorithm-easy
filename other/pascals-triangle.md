# 杨辉三角

### 思路

把杨辉三角看成一个二维数组，找规律可发现。

1. 每行两边的值都是 1；
2. 每行内部的值是上一行对应位置元素和它前一个的元素的和。

### 复杂度

时间复杂度：O(n^2)

空间复杂度：O(1)

### 代码

```php
class Solution {

    /**
     * @param Integer $numRows
     * @return Integer[][]
     */
    function generate($numRows) {
        $output = [];
        for($i = 1; $i <= $numRows; $i++) {
            for($j = 1; $j <= $i; $j++) {
                if($j == 1 || $j == $i) {
                    $output[$i][$j] = 1;
                    continue;
                }

                $output[$i][$j] = $output[$i-1][$j-1] + $output[$i-1][$j];
            }
        }

        return $output;
    }
}
```