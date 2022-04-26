# 打乱数组

### 思路

Fisher-Yates 洗牌算法

遍历数组，把当前元素与随机位置的元素进行交换。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(1)

### 代码

```php
/**
 * Fisher-Yates 洗牌算法
 */
class Solution {
    private $nums;

    /**
     * @param Integer[] $nums
     */
    function __construct($nums) {
        $this->nums = $nums;
    }

    /**
     * Resets the array to its original configuration and return it.
     * @return Integer[]
     */
    function reset() {
        return $this->nums;
    }

    /**
     * Returns a random shuffling of the array.
     * @return Integer[]
     */
    function shuffle() {
        $nums = $this->nums;
        $len = count($nums);
        for($i = 0; $i < $len; $i++) {
            $rIndex = mt_rand(0, $len - 1);
            // 交换
            $temp = $nums[$i];
            $nums[$i] = $nums[$rIndex];
            $nums[$rIndex] = $temp;
        }

        return $nums;
    }
}

/**
 * Your Solution object will be instantiated and called as such:
 * $obj = Solution($nums);
 * $ret_1 = $obj->reset();
 * $ret_2 = $obj->shuffle();
 */
```