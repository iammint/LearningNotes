```js
// check if two objects are equal
function isEqual(obj1, obj2) {
    //遍历一个对象obj1，用相同的i判断与obj2是否相等
    const obj1Keys = Object.keys(obj1)
    const obj2Keys = Object.keys(obj2)
    if(obj1Keys.length !== obj2Keys.length) {
    return false
    }
    for(const i of obj1Keys) {
    if(obj1Keys[i] !== obj2Keys[i]) {
        return false
    }
    }
    return true
}
```