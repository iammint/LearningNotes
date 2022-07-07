# DAY23 Min Number of Brackets Needed to Make a Valid Parenthese String
使括号有效的最少添加
![leetcode921.png](https://media.haochen.me/leetcode921.png)
```js
var minAddToMakeValid = function(s) {
    let ans = 0, bal = 0
    for(const i of s) {
        if(i === "(") {
            bal += 1
        }
        else if(i === ")") {
            bal -= 1
            if(bal < 0) {
                bal = 0
                ans += 1
            }
        }
    }
    return ans+bal
};
```