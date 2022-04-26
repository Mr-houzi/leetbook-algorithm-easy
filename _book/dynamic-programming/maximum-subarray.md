# 最大子序和

## 方法一、贪心算法

### 思路

假设，从第一个元素开始向后遍历累加，得[当前连续子序列和] sum。

当 sum 加上当前元素后，得到新 sum；
若新 sum 大于[最大连续的子序列和] maxSum 时，则更新 maxSum，说明当前遍元素是正数，对 sum 是增益效果；
若新 sum 没有大于 maxSum 时，此时按兵不动，说明当前元素是一个相反数小于 sum 的负数，这个负数对 sum 是减益效果，sum 加上当前元素后变小，但不影响大局；
若新 sum 小于 0 时，说明当前元素是一个相反数大于 sum 的负数，sum 加上当前元素后，全盘皆输。sum 要放弃当前连续序列，从下一元素重新开始累加。

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
    function maxSubArray($nums) {
        // 最大连续的子序列和
        $maxSum = PHP_INT_MIN;
        // 当前连续子序列和
        $sum = 0;

        for($i = 0; $i < count($nums); $i++) {
            $sum = $sum + $nums[$i];
            // 若超过最大连续的子序列和，则更新
            if($sum > $maxSum) {
                $maxSum = $sum;
            }
            // 当前连续和小于0，则需重置，重新连续计算
            if($sum <= 0) {
                $sum = 0;
            }
        }

        return $maxSum;
    }
}
```

## 方法二、动态规划法

### 思路

题外话：@老虎 老哥在[详细解读动态规划的实现, 易理解](https://leetcode-cn.com/problems/maximum-subarray/solution/xiang-xi-jie-du-dong-tai-gui-hua-de-shi-xian-yi-li/)一文中提到，动态规划的核心是“**以子序列的结束点为基准，向前递推子序列关系**”这点，个人感觉对理解动态规划有很大的帮助。

将求 [整个序列最大序列和] 拆分成求 [以a[i]为子序列末端的最大序子列连续和]，**将 [以a[i]为子序列末端的最大序子列连续和]，记为 f(i)**。

若求 [整个序列最大序列和] 则是求 i 取 [0, len -1]时，f(i) 的最大值。

**如何求 f(i)？**

f(i) 与 f(i-1) 、a[i] 有关。[以a[i-1]为子序列末端的最大序子列连续和]，即 f(i-1) 加上当前元素 a[i]后，

若“和”增加，f(n-1) 对 a[i]是增益效果，则 f(n-1) + a[i] 作为 f(i) 的值；
若“和”减少，f(n-1) 对 a[i]是减益效果，则抛弃 f(n-1)，直接取 a[i] 作为 f(i)。 

所以可以得到动态转移方程：

    f(i) = max( f(i-1) + a[i], a[i] )

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
    function maxSubArray($nums) {
        // 最大和 
        $max = PHP_INT_MIN;
        // 记录以a[i]为子序列末端的最大序子列连续和
        $sum = 0;
        for($i = 0; $i < count($nums); $i++) {
            $sum = max($sum + $nums[$i], $nums[$i]);
            $max = max($sum, $max);
        }

        return $max;
    }
}
```