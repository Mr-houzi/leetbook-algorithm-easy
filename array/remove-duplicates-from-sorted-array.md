# [26. 删除有序数组中的重复项](https://leetcode.cn/problems/remove-duplicates-from-sorted-array/)

### 思路

双指针法。


指针 i 和 j 一前一后，比较对应的值；

若相等，则删除 j 对应的值，j 继续向后移动一位；

若不相等，i 需要移动到 j 的位置，j 向后移动一位；

如此反复，直到 j 到达数组最后。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function removeDuplicates(&$nums) {
        $len = count($nums);
        for($i = 0, $j = 1; $j < $len;) {
            if($nums[$i] === $nums[$j]) {
                unset($nums[$j]);
                $j++;
            } else {
                $i = $j;
                $j++;
            }
        }

        return count($nums);
    }
}
```