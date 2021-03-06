# 字符串中的第一个唯一字符

### 思路

哈希表法，题目要求的是返回第一个唯一字符串的 key ，而不是 value ，所以 hash 每个 item 中，既要存出现次数，也要存储在字符串中的键值。

当然，仅存次数也可以，再另外遍历一次字符串，判断字符出现的位置即可，复杂度相同。

### 复杂度

时间复杂度：O(n)

空间复杂度：O(m)

m 唯一的字符串个数, m < n

### 代码

```
class Solution {

    /**
     * @param String $s
     * @return Integer
     */
    function firstUniqChar($s) {
        $hash = [];
        for($i = 0; $i < strlen($s); $i++) {
            if(isset($hash[$s[$i]]['count'])) {
                $hash[$s[$i]]['count'] += 1;
            } else {
                $hash[$s[$i]]['count'] = 1;
                $hash[$s[$i]]['key'] = $i;
            }
        }

        foreach($hash as $value) {
            if($value['count'] == 1) {
                return $value['key'];
            }
        }

        return -1;
    }
}
```