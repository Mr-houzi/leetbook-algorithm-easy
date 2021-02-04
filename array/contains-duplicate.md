# 存在重复元素

## 一、哈希表法

### 思路

利用哈希表，以 key 为元素值， value 为元素个数，若 key 已在 hash 中存在，则表示 nums 有重复值。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(n)

### 代码

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Boolean
     */
    function containsDuplicate($nums) {
        $hash = [];
        for($i = 0; $i < count($nums); $i++){
            if(array_key_exists($nums[$i], $hash)) {
                return true;
            } else {
                $hash[$nums[$i]] = 1;
            }
        }

        return false;
    }
}
```

## 二、排序法

### 思路

利用内置函数快排，然后遍历比较前后值是否相同。

### 复杂度

sort() 内置函数一般被认为是快速排序，时间和空间复杂度都来自于快速排序。

时间复杂度：O(nlogN)

空间复杂度：O(nlogN)

### 代码

```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Boolean
     */
    function containsDuplicate($nums) {
        // 利用内置函数快排
        sort($nums);
        for($i = 0; $i < count($nums) - 1; $i++){
            if($nums[$i] == $nums[$i+1]) return true;
        }

        return false;
    }
}
```

PS: 利用冒泡等其他时间性能不佳的排序，可以把空间复杂度降到最低。