# 移动零

### 思路

常规思路，遍历数组，若元素为 0 则删除，并在数组末尾增加 0 元素。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return NULL
     */
    function moveZeroes(&$nums) {
        // 0 的个数
        $counter = 0;
        $len = count($nums);
        for($i = 0; $i < $len; $i++) {
            if($nums[$i] == 0) {
                $counter++;
                unset($nums[$i]);
                $nums[$len - 1 + $counter] = 0;
            }
        }

        return $nums;
    }
}
```