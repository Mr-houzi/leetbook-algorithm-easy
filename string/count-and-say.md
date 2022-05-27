# [38. 外观数列](https://leetcode.cn/problems/count-and-say/)

### 思路

递归法

欲求 n = 4，需要先知道 n = 3 的结果，在对其结果进行“读”操作，然后返回，由此递归；
递归的尽头是 n = 1，返回 1；n = 2，返回 11。

如何进行“读”操作？

遍历比较当前元素和前一个元素是否相等，若相等则计数+1；
若不相等，则进行对前面的连续元素进行“读”，并将计数器重置为1。

**“读”操作并不复杂，但遍历时边界问题的比较处理起来比较难受。**

当 n = 2，返回时字符串长度为2。遍历时，从 i = 1 开始，可以解决当前元素i = 0和前一个元素比较产生的**前边界问题**。

当 n 为最后一个元素时且不等于前一个元素时，需要对前面的连续元素进行“读”，然后结束循环，则无法将最后一个元素“读”出。对于这个问题，在不增加额外判断的情况下，可以在遍历前对字符串尾部增加一个哨兵（拼上一个当前字符串不可能出现的字符，例如：a），这样来解决**后边界问题**。

### 复杂度

时间复杂度：O(n^2)

空间复杂度：O(1)

### 代码

```
class Solution {

    /**
     * @param Integer $n
     * @return String
     */
    function countAndSay($n) {
        return $this->helper($n);
    }

    function helper($n){
        if($n == 1) return '1';

        if($n == 2) return '11';

        $value = $this->helper($n-1);
        $value .= 'a'; // 结尾加个哨兵

        $sayValue = '';
        $counter = 1;
        for($i = 1; $i < strlen($value); $i++) {
            if($value[$i] == $value[$i-1]) {
                $counter++;
            } else {
                // 读
                $sayValue .= $counter.$value[$i-1];
                $counter = 1;
            }
        }

        return $sayValue;
    }
}
```