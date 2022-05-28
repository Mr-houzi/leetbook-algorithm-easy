# [268. 丢失的数字](https://leetcode.cn/problems/missing-number/)

## 方法一、键值交换

### 思路

这个题很容易想到借助一个单独的hash表来做，但时并不能满足进阶要求中的空间复杂度要为O(1)。所以不能借助新的辅助数组。

键值交换

1. 数组 key ，value 交换位置；
2. 遍历交换后的数组，判断哪个key没有，即为缺失的值。

PS：此法用下列代码维持O(1)的空间复杂度，有些取巧的嫌疑。操作整型数组变成关联数组，这在PHP可以说得通。对于强类型语言来说，就很难实现了，并不能保证O(1)的空间复杂度。

```php
$nums['L'.$nums[$i]] = $i;
unset($nums[$i]);
```

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```php
class Solution {

    /**
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

## 方法二、数学法

### 思路

利用**高斯求和公式**。

nums 是包含 [0, n] 的 n 个元素的数组，有一个 [0, n] 范围数没出现在这个数组中。

计算 0,1,2,3……n-1,n 数列的和，然后减去 nums 数组整数和，则得到缺失数字的值。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function missingNumber($nums) {
        $n = count($nums);
        $sum = (1 + $n) * $n / 2;
        
        return $sum - array_sum($nums);
    }
}
```