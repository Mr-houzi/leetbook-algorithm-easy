# 验证回文串

### 思路

双指针法，一个指针（i）从头，一个指针（j）从尾，进行遍历比较，当指针索引i大于指针索引j时，遍历结束。

题目中提到仅判断字母和数字且字母忽略大小写，可以借助PHP的两个内置函数实现。

- ctype_alnum 验证字符是否仅含字母和（或）数字 
- strcasecmp 比较字符（忽略字母大小写）

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```
class Solution {

    /**
     * @param String $s
     * @return Boolean
     */
    function isPalindrome($s) {
        $len = strlen($s);
        for($i = 0, $j = $len - 1; $i < $j;){
            if(!ctype_alnum($s[$i])) {
                $i++;
                continue;
            }

            if(!ctype_alnum($s[$j])) {
                $j--;
                continue;
            }

            if(strcasecmp($s[$i], $s[$j]) != 0) {
                return false;
            } else {
                $i++;
                $j--;
            }
        }

        return true;
    }
}
```