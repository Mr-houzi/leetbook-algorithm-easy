# [344. 反转字符串](https://leetcode.cn/problems/reverse-string/)

### 思路

双指针

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```
class Solution {

    /**
     * @param String[] $s
     * @return NULL
     */
    function reverseString(&$s) {
        for($i = 0, $j = count($s) -1; $i < $j; $i++, $j--) {
            $tmp = $s[$i];
            $s[$i] = $s[$j];
            $s[$j] = $tmp;
        }

        return $s;
    }
}
```