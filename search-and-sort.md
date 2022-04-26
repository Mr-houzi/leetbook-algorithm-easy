# 查找和排序

常见的查找和排序

## 查找

### 顺序查找

顾名思义，按线性顺序遍历即可。

### 二分（折半）查找

适用于有序的顺序表，不适用于链表。

基本思路：
先将给定值 target 与有序表中中间位置（mid）的元素比较；
若 target 与中心元素相等，则查找成功，返回该元素的索引；
若 target 小于中心元素，则以[low, mid -1]的索引范围内继续按上述查找；
若 target 大于中心元素，则以[mid + 1, hight]的索引范围内继续按上述查找。
当 low = hight 时，则查找完毕。

```php
class Solution {

    function binarySearch($arr, $target) {
        $low = 0;
        $hight = count($arr) - 1;
        while($low <= $hight) {
            $mid = $low + intval(($hight - $low) / 2);

            if($target == $arr[$mid]) {
                return $mid;
            } else if($target < $arr[$mid]){
                $hight = $mid -1;
            } else {
                $low = $mid + 1;
            }
        }

        return -1;
    }
}
```

### 分块查找

吸取了顺序查找和二分查找的各自优点，实现了块外二分、块内顺序查找。

## 排序

### 插入排序

#### 直接插入排序

#### 折半插入排序

#### 希尔排序

### 交换排序