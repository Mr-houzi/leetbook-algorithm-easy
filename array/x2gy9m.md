```
class Solution {

    /**
     * @param Integer[] $nums
     * @return Integer
     */
    function removeDuplicates(&$nums) {
        $len = count($nums);
        for($i = 0, $j = 1; $j < $len;) {
            if($nums[$i] === $nums[$j]) {
                unset($nums[$j]);
                $j++;
            } else {
                $i = $j;
                $j++;
            }
        }

        return count($nums);
    }
}
```