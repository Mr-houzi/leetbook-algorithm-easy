# 打家劫舍

### 思路

动态规划

将求整个打劫的最大金额拆分为求若干个遍历到i时的最大打劫金额，并记为f(i)。

若求整个打劫的最大金额则变成了求 i 取 [0, len] 时，f(i) 的最大值。

**如何求 f(i) ?**

分析：遍历到 i 点的最大打劫金额 f(i) 取决于 f(i-1) 、f(i-2) 、nums[i]。
一种情况是不打劫 nums[i] ，那么 f(i) 就等于 f(i-1)；
另一种情况则是打劫 nums[i] ， 打劫了nums[i]，则必然不能打劫 nums[i-1]，那么 f(i) 就等于 f(i-2) + nums[i]。最终，取两种情况的最大值，作为 f(i)。

由此可得动态转移方程：

    f(i) = max(f(i-2) + nums[i], f(i-1))


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
    function rob($nums) {
        if(count($nums) == 1) return $nums[0];
        if(count($nums) == 2) return max($nums[0], $nums[1]);

        $hash = [
            $nums[0],
            max($nums[0], $nums[1])
        ];
        for($i = 2; $i < count($nums); $i++) {
            $hash[$i] = max($hash[$i-2] + $nums[$i], $hash[$i-1]);
        }

        return max($hash);
    }
}
```

上面这段代码利用了长度为 n 的空间复杂度来存储遍历到 i 时的最大打劫金额，实际上每次用到的，只是是 i - 1，i -2 的最大打劫金额，即 f(i-1)，f(i-2)。可以用**利用三个滑动变量**将其空间复杂度优化至O(1)。

```php
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function rob($nums) {
        // 全局最大打劫金额
        $max = 0;

        // 滑动块
        $p1 = 0;
        $p2 = 0;
        $p3 = 0;
        
        for($i = 0; $i < count($nums); $i++) {
            $p3 = max($p1 + $nums[$i], $p2);
            $max = max($max, $p3);
            // 向后滑动
            $p1 = $p2;
            $p2 = $p3;
        }
        return $max;
    }
}
```