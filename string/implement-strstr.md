# [28. 实现 strStr()](https://leetcode.cn/problems/implement-strstr/)

### 思路

双指针法，利用两个指针分别遍历两个字符串进行比较。
当值相等时，两指针分别递增；
当值不相等时，haystack 的指针 i 需要回溯到 i - j + 1的位置，j 重置为0，再进行重新比较。

注意处理两种特殊情况：
1. needle 为 '' 时，始终返回 0
2. haystack 长度小于 needle 时，一定搜索不到，直接返回 -1

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```php
class Solution {

    /**
     * @param String $haystack
     * @param String $needle
     * @return Integer
     */
    function strStr($haystack, $needle) {

        if($needle == '') return 0;
        if(strlen($haystack) < strlen($needle)) return -1;

        $hLen = strlen($haystack);
        $nLen = strlen($needle);

        for($i = 0, $j = 0; $i < $hLen && $j < $nLen;) {
            if($haystack[$i] == $needle[$j]) {
                $i++;
                $j++;
            } else {
                // i 回溯，j 重置为0
                $i = $i - $j + 1;
                $j = 0;
            }
            
            if($j == $nLen) return $i - $j;
        }

        return -1;
    }
}
```