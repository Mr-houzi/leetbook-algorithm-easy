# 字符串转换整数 (atoi)

### 思路

字符类型分为空格、符合、数字、字母四种情况。

遍历时先区别前面「有数字或符号」和「无数字或符号」这两大类；
然后再细分，分别处理四种情况。

详细解答见代码

### 复杂度

时间复杂度：O(n)

空间复杂度：O(m)

### 代码

```php
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function myAtoi($s) {
        // 数字栈
        $stack = [];
        // 符号位
        $operator = '';
        $num = 0;

        // 1. 筛出有效数字入栈，暂存符号
        for($i = 0; $i < strlen($s); $i++){
            /**
             * 当前面已经有数字或者符号时，则当前不能存在空格、符号，则返回退出循环；
             * 当前面已经不存在数字或者符号时，则当前若存在空格、符号，则进入下一循环；
             * 无论何时都不能存在字符字母，碰到字符串直接退出循环；
             * 无论何时碰到字符数字，则压入数字栈。
             */
            if(count($stack) !== 0 || $operator !== ''){
                if($s[$i] === ' ') break;

                if($s[$i] == '-' || $s[$i] == '+') break;

                if(is_numeric($s[$i])) {
                    $stack[] = $s[$i];
                    continue;
                }

                if(is_string($s[$i])) break;
            } else {
                if($s[$i] === ' ') continue;

                if($s[$i] == '-' || $s[$i] == '+') {
                    $operator = $s[$i];
                    continue;
                }

                if(is_numeric($s[$i])) {
                    $stack[] = $s[$i];
                    continue;
                }

                if(is_string($s[$i])) break;
            }
        }

        // 2. 出栈逐位相加
        $sLen = count($stack);
        for($i = $sLen-1; $i >= 0; $i--){
            $num += $stack[$i] * pow(10, $sLen - 1 - $i);
        }

        // 3. 确定符号
        if($operator == '-') {
            $num = -$num;
        }
        
        // 4. 是否越界
        if($num > pow(2, 31) - 1){
            return pow(2, 31) -1;
        }

        if($num < -pow(2, 31)){
            return -pow(2, 31);
        }

        return $num;
    }
}
```