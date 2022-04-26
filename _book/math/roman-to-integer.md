# 罗马数字转整数

### 思路

1. 将所有表示情况列出来
2. 遍历相加，只有两种情况。1. 单个字符，2. 两个字符

由于传入的测试用例都是合法的，所以不用判断跨位情况，难度大大降低。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```php
class Solution {

    /**
     * 
     * @param String $s
     * @return Integer
     */
    function romanToInt($s) {
        $hash = [
            "I" => 1,
            "V" => 5,
            "X" => 10,
            "L" => 50,
            "C" => 100,
            "D" => 500,
            "M" => 1000,
            "IV" => 4,
            "IX" => 9,
            "XL" => 40,
            "XC" => 90,
            "CD" => 400,
            "CM" => 900
        ];

        $sum = 0;

        for($i = 0; $i < strlen($s);){
            if(isset($s[$i+1]) && isset($hash[$s[$i].$s[$i+1]])) {
                $sum += $hash[$s[$i].$s[$i+1]];
                $i = $i + 2;
            } else {
                $sum += $hash[$s[$i]];
                $i++;
            }
        }

        return $sum;
    }
}
```