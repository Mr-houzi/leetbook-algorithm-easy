# 旋转数组

## 方法一 常规法

### 思路

尾出头进

### 复杂度

array_unshift 移动的时间复杂度为 n

时间复杂度：O(k*n)

空间复杂度：O(1)

### 代码

```
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $k
     * @return NULL
     */
    function rotate(&$nums, $k) {
        $i = 0;
        while($i < $k) {
            $value = array_pop($nums);
            array_unshift($nums, $value);
            $i++;
        }

        return $nums;
    }
}
```

## 方法二 多次反转法

### 思路

将倒数 k 个元素是为组B，前面的元素为组A。分别反转组A，组B，最后再反转整体即可。

注意处理一下：k 大于数组长度的问题。

### 复杂度

array_unshift 移动的时间复杂度为 n

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $k
     * @return NULL
     */
    function rotate(&$nums, $k) {

        $len = count($nums);
        // 当 k 大于 数组的长度，相当于只需要移动余数位
        $k = $k % $len;

        $this->reverse($nums, 0, $len - $k -1);
        $this->reverse($nums, $len - $k, $len - 1);
        $this->reverse($nums, 0, $len -1);

        return $nums;
    }

    /**
     * $arr 数组
     * $start $end 确定那段区间进行反转
     */
    function reverse(&$arr, $start, $end)
    {
        for(;$start < $end; $start++, $end--) {
            $temp = $arr[$start];
            $arr[$start] = $arr[$end];
            $arr[$end] = $temp;
        }
    }
}
```