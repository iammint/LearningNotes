# DAY46 二进制搜索计算以二为基数的对数函数
```js
function log2(x) {
    if(x <= 0) {
        return null
    }
    if(x < 1) {
        return -log2(1/x)
    }
    let low = 0
    let high = x
    let middle = null
    let current = Math.pow(2, (low+high)/2)
    while(Math.abs(current - x) > 1e-5) {
        middle = (low + high)/2
        
        current = Math.pow(2, middle)
        if(current >= x) {
            high = middle
        } else {
            low = middle
        }
    }
    return middle
}
console.log(log2(1));
console.log(log2(32));
console.log(log2(1024));
```