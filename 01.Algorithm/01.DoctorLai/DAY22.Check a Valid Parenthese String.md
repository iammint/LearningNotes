# DAY22 Check a Valid Parenthese String
判断有效括号匹配
```js
function valid(str) {
    let b = 0
    for(let i=0; i<str.length; i++) {
        if(str[i] == "(") {
            b += 1
        } else if(str[i] == ")") {
            b -= 1
        }
    }
    if(b === 0) {
        return true
    }else {
        return false
    }
}
console.log(valid("()()()((("))
```
![leetcode20.png](https://media.haochen.me/leetcode20.png)
```js
var isValid = function(s) {
    const stack = []
    for(const i of s) {
        if(i === "(") {
            stack.push(")")
        }
        else if(i === "{") {
            stack.push("}")
        }
        else if(i === "[") {
            stack.push("]")
        }
        else {
            if(i != stack.pop()) return false
        }
    }
    return !stack.length
};
```