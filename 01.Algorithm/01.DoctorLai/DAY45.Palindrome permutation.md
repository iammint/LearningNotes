# DAY45 Palindrome permutation 回文全排列
全排列123有3!种排列方法
## Leetcode 01.04
```js
//判断是否可以进行回文全排列
var canPermutePalindrome = function(s) {
    //判断每个字母出现的次数，最多只能有一个字母出现单数的次数
    //如果是短语要将空格去除
    s = s.replace(' ', '')
    let recordNum = {}
    for(let i of s) {
        if(recordNum[i]) {
            recordNum[i]++
        } else {
            recordNum[i] = 1
        }
    }
    let it = Object.values(recordNum)
    let ans = 0
    for(let num of it) {
        if(num % 2 === 1) {
            ans++
        }
    }
    return ans > 1 ? false : true
};
```