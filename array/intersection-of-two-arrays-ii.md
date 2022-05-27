# [350. 两个数组的交集 II](https://leetcode.cn/problems/intersection-of-two-arrays-ii/)

## 方法一、排序+双指针

### 思路

使用 sort 函数（快排），然后利用双指针，比较两个数组中相同的值。

### 复杂度

时间复杂度：O(max(nlogn, mlogm))

空间复杂度：O(min(n, m)) ，其他语言中数组需要提前声明固定长度。

### 代码

```
class Solution {

    /**
     * @param Integer[] $nums1
     * @param Integer[] $nums2
     * @return Integer[]
     */
    function intersect($nums1, $nums2) {
        sort($nums1);
        sort($nums2);
        $result = []; 
        for($i = 0, $j = 0; $i < count($nums1) && $j < count($nums2);) {
            if($nums1[$i] == $nums2[$j]) {
                $result[] = $nums1[$i];
                $i++;
                $j++;
            } else if($nums1[$i] > $nums2[$j]) {
                $j++;
            } else {
                $i++;
            }
        }

        return $result;
    }
}
```

## 方法二、哈希表

### 思路

利用哈希表，将数组一记录到哈希表中，哈希表的 key 为数组的元素，value 为该元素出现的次数。数组一记录到哈希表这个动作类似于一个生产者。

数组二扮演消费者的角色。遍历数组二，若数组二元素中有和哈希表中 key 相同且出现次数（value）大于0，则将哈希表对应次数减一，并输出。

### 复杂度

时间复杂度：O(max(n, m))

空间复杂度：O(min(n, m))

### 代码

```
class Solution {

    /**
     * @param Integer[] $nums1
     * @param Integer[] $nums2
     * @return Integer[]
     */
    function intersect($nums1, $nums2) {
        $hash = [];
        $result = [];

        // 遍历 $nums1 放入 hash
        for($i = 0; $i < count($nums1); $i++) {
            if(isset($hash[$nums1[$i]])) {
                $hash[$nums1[$i]]++;
            } else {
                $hash[$nums1[$i]] = 1;
            }
        }

        // 遍历 $nums2 ，若 nums2 中有和哈希表中 key 相同且出现次数大于0，则将哈希表对应值减一，并输出。
        for($i = 0; $i < count($nums2); $i++) {
            if(isset($hash[$nums2[$i]]) && $hash[$nums2[$i]] > 0) {
                $hash[$nums2[$i]]--;
                $result[] = $nums2[$i];
            }
        }

        return $result;
    }
}
```