# [36. 有效的数独](https://leetcode.cn/problems/valid-sudoku/)

### 思路

暴力法

1. 判断同行有无重复
2. 判断同列有无重复
3. 判断3*3方块内有无重复

如何确定3*3方块最右上角位置？

```
$blockX = floor($i / 3) * 3;
$blockY = floor($j / 3) * 3;
```

### 复杂度

时间复杂度：O(n^2)

空间复杂度：O(1)

### 代码

```
class Solution {

    /**
     * @param String[][] $board
     * @return Boolean
     */
    function isValidSudoku($board) {
        for($i = 0; $i < 9; $i++) {
            for($j = 0; $j < 9; $j++) {
    
                if($board[$i][$j] == '.') continue;

                /**
                 * 1. 判断同行有无重复
                 */
                
                for($col = 0; $col < 9; $col++) {
                    if($j != $col && $board[$i][$j] == $board[$i][$col]) {
                        return false;
                    }
                }

                /**
                 * 2. 判断同列有无重复
                 */
    
                for($row = 0; $row < 9; $row++) {
                    if($i != $row && $board[$i][$j] == $board[$row][$j]) {
                        return false;
                    }
                }
    
                /**
                 * 3. 判断9*9方块内有无重复
                 */

                $blockX = floor($i / 3) * 3;
                $blockY = floor($j / 3) * 3;
    
                if($i != $blockX && $j != $blockY && $board[$i][$j] == $board[$blockX][$blockY]) return false;
                if($i != $blockX && $j != $blockY+1 && $board[$i][$j] == $board[$blockX][$blockY+1]) return false;
                if($i != $blockX && $j != $blockY+2 && $board[$i][$j] == $board[$blockX][$blockY+2]) return false;
                if($i != $blockX+1 && $j != $blockY && $board[$i][$j] == $board[$blockX+1][$blockY]) return false;
                if($i != $blockX+1 && $j != $blockY+1 && $board[$i][$j] == $board[$blockX+1][$blockY+1]) return false;
                if($i != $blockX+1 && $j != $blockY+2 && $board[$i][$j] == $board[$blockX+1][$blockY+2]) return false;
                if($i != $blockX+2 && $j != $blockY && $board[$i][$j] == $board[$blockX+2][$blockY]) return false;
                if($i != $blockX+2 && $j != $blockY+1 && $board[$i][$j] == $board[$blockX+2][$blockY+1]) return false;
                if($i != $blockX+2 && $j != $blockY+2 && $board[$i][$j] == $board[$blockX+2][$blockY+2]) return false;
            }
        }
    
        return true;
    }
}
```