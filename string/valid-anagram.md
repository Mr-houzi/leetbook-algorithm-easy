# [242. 有效的字母异位词](https://leetcode.cn/problems/valid-anagram/)

### 思路

字母异位词：使用字母相同和相同字母的个数也相同，构成不同的单词。

利用哈希表+生产消费的概念。
1. 遍历第一个单词，将所有的字符存储哈希表中，并记录次数（视为生产者）；
2. 遍历第二个单词，若当前字符在哈希表中存在，此字符在哈希表中的次数减一（视为消费者）；
若不存在，则两个单词不是异位词；
3. 遍历哈希表，判断每个元素的值是否为0，若为0，则证明全部消费掉，即两个单词是异位词；
若存在有不为0的，则没全部消费掉，即两个单词不是异位词。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(m)

### 代码

```
class Solution {

    /**
     * @param String $s
     * @param String $t
     * @return Boolean
     */
    function isAnagram($s, $t) {
        $hash = [];
        // 生产
        for($i = 0; $i < strlen($s); $i++) {
            if(isset($hash[$s[$i]])) {
                $hash[$s[$i]] += 1;
            } else {
                $hash[$s[$i]] = 1;
            }
        }

        // 消费
        for($i = 0; $i < strlen($t); $i++) {
            if(isset($hash[$t[$i]])) {
                $hash[$t[$i]] -= 1;
            } else {
                return false;
            }
        }

        // 判断hash中的每个字母是否全部消费掉
        foreach($hash as $value) {
            if($value != 0 ) {
                return false;
            }
        }

        return true;
    }
}
```