# 旋转图像

### 思路

上下翻转 + 主对角线翻转 = 旋转图像

### 复杂度

时间复杂度：O(n^2)

空间复杂度：O(1)

### 代码

```
class Solution {

    /**
     * @param Integer[][] $matrix
     * @return NULL
     */
    function rotate(&$matrix) {
        $len = count($matrix);

        // 上下翻转
        for($i = 0; $i < intval($len/2); $i++) {
            for($j = 0; $j < $len; $j++) {
                $tmp = $matrix[$i][$j];
                $matrix[$i][$j] = $matrix[$len - 1 - $i][$j];
                $matrix[$len - 1 - $i][$j] = $tmp;
            }
        }

        // 主对角线翻转
        for($i = 0; $i < $len; $i++) {
            for($j = 0; $j < $len; $j++) {
                if($j > $i) {
                    $tmp = $matrix[$i][$j];
                    $matrix[$i][$j] = $matrix[$j][$i];
                    $matrix[$j][$i] = $tmp;
                }
            }
        }

        return $matrix;
    }
}
```