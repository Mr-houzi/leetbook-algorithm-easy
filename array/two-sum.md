# 两数之和

## 方法一、暴力法

### 思路

双层遍历

### 复杂度

时间复杂度：O(n^2)

空间复杂度：O(1)

### 代码

```
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($nums, $target) {
        for($i = 0; $i < count($nums); $i++) {
            $diff = $target - $nums[$i];
            for($j = 0; $j < count($nums); $j++) {
                if($diff == $nums[$j] && $i != $j) {
                    return [$i, $j];
                }
            }
        }
    }
}
```

## 方法二、哈希表法

### 思路

暴力法的瓶颈在于寻找差diff的时间复杂度过高，为 O(n)，可以将 nums 键值交换后存到 hash 中。这样查找 diff 的时间复杂度就变为了 O(1)。

特别注意，题目要求不能使用同一个元素。元素值相同没关系，只要保证元素对应的 key 不同即可。

即，输入测试用例 nums = [3,3], target = 6，结果不能是[0, 0] 或 [1, 1]，但可以是[0, 1]

### 复杂度

时间复杂度：O(n)

空间复杂度：O(n)

### 代码

```
class Solution {

    /**
     * @param Integer[] $nums
     * @param Integer $target
     * @return Integer[]
     */
    function twoSum($nums, $target) {
        // 键值交换
        $hash = array_flip($nums);

        // 根据 target - num 结果查找对应的键值的复杂度将为 O(1)
        for($i = 0; $i < count($nums); $i++) {
            $diff = $target - $nums[$i];
            if(isset($hash[$diff]) && $i !== ($hash[$target - $nums[$i]]) ) {
                return [$i, $hash[$target - $nums[$i]]];
            }
        }
    }
}
```