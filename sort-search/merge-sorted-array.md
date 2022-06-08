# [88. 合并两个有序数组](https://leetcode.cn/problems/merge-sorted-array/)

### 思路

双指针法。

利用双指针从尾部遍历，即 nums1 从 m - 1 处向前，nums2 从 n - 1 处向前。

由于 nums1 已经开辟了足够的空间，遍历两个数组时比较谁大，谁插入 nums1 的尾部。

可能会出现一种特殊情况，nums1 的 m 指针已经到 -1 了，但 nums2 的 n 指针还没遍历完，最后直接把他塞入 nums1 中即可。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```php
class Solution {

    /**
     * @param Integer[] $nums1
     * @param Integer $m
     * @param Integer[] $nums2
     * @param Integer $n
     * @return NULL
     */
    function merge(&$nums1, $m, $nums2, $n) {
        $i = count($nums1) -1;

        $m = $m - 1;
        $n = $n - 1;
        while($m >=0 && $n >= 0) {
            if($nums1[$m] >= $nums2[$n]) {
                $nums1[$i] = $nums1[$m];
                $m--;
            } else {
                $nums1[$i] = $nums2[$n];
                $n--;
            }

            $i--;
        }

        if($n >= 0) {
            while($n >= 0) {
                $nums1[$i] = $nums2[$n];
                $n--;
                $i--;
            }
        }

        return $nums1;
    }
}
```