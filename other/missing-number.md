# 缺失数字

### 思路

这个题很容易想到借助一个单独的hash表来做，但时并不能满足进阶要求中的空间复杂度要为O(1)。所以不能借助新的辅助数组。

键值交换

1. 数组 key ，value 交换位置；
2. 遍历交换后的数组，判断哪个key没有，即为缺失的值。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```php
class Solution {

    /**
     * 时间复杂度O（n）
     * 空间复杂度O（1）
     * @param Integer[] $nums
     * @return Integer
     */
    function missingNumber($nums) {
        // 键值交换
        for($i = 0; $i < count($nums); $i++) {
            $nums['L'.$nums[$i]] = $i;
            unset($nums[$i]);
        }

        // 遍历判断key是否存在
        for($i = 0; $i <= count($nums); $i++) {
            if(!isset($nums['L'.$i])) return $i;
        }
    }
}
```