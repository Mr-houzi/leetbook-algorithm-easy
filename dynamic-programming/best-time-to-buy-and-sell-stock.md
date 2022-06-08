# [121. 买卖股票的最佳时机](https://leetcode.cn/problems/best-time-to-buy-and-sell-stock/)

### 思路

最低价时买入，与最低价差价最大时卖出。

### 复杂度

时间复杂度：O(n)

空间复杂度：O()

### 代码

```php
class Solution {

    /**
     * @param Integer[] $prices
     * @return Integer
     */
    function maxProfit($prices) {
        $minPrice = PHP_INT_MAX;
        $maxProfit = 0;
        for($i = 0; $i < count($prices); $i++){
            if($prices[$i] < $minPrice) { // 动态确定买入点
                $minPrice = $prices[$i]; 
            } elseif($prices[$i] - $minPrice > $maxProfit) { // 与最低价差价最大时，更新最大收益
                $maxProfit = $prices[$i] - $minPrice;
            }
        }

        return $maxProfit;
    }
}
```

# 系列题目

- [数组-买卖股票的最佳时机 II](../array/best-time-to-buy-and-sell-stock-ii.md)
- [动态规划-买卖股票的最佳时机](../dynamic-programming/best-time-to-buy-and-sell-stock.md)

- **买卖股票的最佳时机 II** 可以多次买入多次卖出，这样的话，实际上就是求前后两个上升数的和，无需确定买入点。
- **买卖股票的最佳时机** 只能买入一次，相当于全局控制最大收益，需要确定买入点。