# DAY6 How to check if a string has all unique characters?

> 传统方法：使用一个集合set来记录在字符串中出现过的字符，如果我们发现一个已经在集合中的字符，则检查失败。
```js
function isUnique(s) {
    const st = new Set(s);
    for(const i of s){
        if(st.has(i)) return false
        set.add(i)
    }
    return true
}
```

> 更好的方法：
> 
> 检查集合set与字符串的长度是否一致
```js
function isUnique(s) {
    return new Set(s).size === s.length;
}
```
