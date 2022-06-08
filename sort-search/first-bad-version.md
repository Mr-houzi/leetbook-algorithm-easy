# [278. 第一个错误的版本](https://leetcode.cn/problems/first-bad-version/)

### 思路

典型的二分查找

### 复杂度

时间复杂度：O(logn)

空间复杂度：O(1)

### 代码

```php
/* The isBadVersion API is defined in the parent class VersionControl.
      public function isBadVersion($version){} */

      class Solution extends VersionControl {
        /**
         * 二分法
         * @param Integer $n
         * @return Integer
         */
        function firstBadVersion($n) {
            $low = 1;
            $hight = $n;
            while($low < $hight) {
                $mid = $low + intval(($hight - $low) / 2);
                if($this->isBadVersion($mid)) {
                    $hight = $mid;
                } else {
                    $low = $mid + 1;
                }
            }
    
            return $low;
        }
    }
```