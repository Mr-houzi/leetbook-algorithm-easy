# 最长公共前缀

## 方法一、横向比较

### 思路

最长公共前缀一定是数组元素都具有的，默认当前最长公共前缀为第一个元素值，进行遍历，拿第一个、第二个……分别与当前最长公共前缀比较，逐步最小最长公共前缀的范围，最终确定最长公共前缀。

### 复杂度

时间复杂度：O(nm)

n 元素个数，m平均每个元素的字符长度。

空间复杂度：O(1)

### 代码

```php
class Solution {

    /**
     * @param String[] $strs
     * @return String
     */
    function longestCommonPrefix($strs) {
        // 当前最大前缀
        $prefix = '';
        for($i = 0, $prefix = $strs[0] ? : ''; $i < count($strs); $i++) {
            for($j = 0; $j < strlen($prefix); $j++) {
                if($prefix[$j] != $strs[$i][$j]) {
                    $prefix = substr($prefix, 0, $j);
                    break;
                }
            }
        }

        return $prefix;
    }
}
```

## 方法二、纵向比较

### 思路

判断每个元素中的第一个字符是否相同，第二个字符是否相同……当有不相同或者有元素字符遍历完毕，则结束。

### 复杂度

时间复杂度：O(nm)

n 元素个数，m平均每个元素的字符长度。

空间复杂度：O(1)

### 代码

```
class Solution {

    /**
     * @param String[] $strs
     * @return String
     */
    function longestCommonPrefix($strs) {

        if(empty($strs)) return '';

        // 元素的最小长度
        $mixLen = PHP_INT_MAX;
        for($i = 0; $i < count($strs); $i++) {
            if(strlen($strs[$i]) < $mixLen) {
                $mixLen = strlen($strs[$i]);
            }
        }

        // 当前最大前缀
        $prefix = '';
        $i = 0;

        while($i < $mixLen) {
            $curStr = $strs[0][$i];
            for($j = 0; $j < count($strs); $j++) {
                if($strs[$j][$i] != $curStr) {
                    break 2;
                }
            }
            
            $prefix .= $curStr ? : '';
            $i++;
        }

        return $prefix;
    }
}
```