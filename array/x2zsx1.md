## 买卖股票的最佳时机 II

### 思路

贪心算法。

可多次买入，最低点买，最高点买，再买在卖。

利用贪心算法，判断一下买入当前点 i 之后对总收益有没有增益，若有则买；

否则不买，且 i - 1 为卖出点，在 i 点重新买入。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```
class Solution {

    /**
     * @param Integer[] $prices
     * @return Integer
     */
    function maxProfit($prices) {
        // 最大收益
        $max = 0;
        for($i = 1; $i < count($prices); $i++) {
            // 计算一下若买入当前点i之后的总收益
            $newMax = $max + $prices[$i] - $prices[$i-1];
            // 若大于则选择买入，更新最大收益；否则不买，且 i-1 为卖出点，在 i 点重新买入。
            if($newMax > $max) {
                $max = $newMax;
            }
        }

        return $max;
    }
}
```