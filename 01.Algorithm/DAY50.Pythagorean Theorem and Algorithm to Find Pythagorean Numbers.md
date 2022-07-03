# DAY50 寻找勾股定理数的算法
已知c找出满足勾股定理的a和b
```js
function pytha(c) {
    let a = 1
    //b^2 = c^2 - a^2
    //b^2 >= a^2
    //while(b*b>= a*a)
    while(c*c >= 2*a*a) {
        let b2 = c*c - a*a
        let b = parseInt(Math.sqrt(b2))
        //筛选掉非整数的Math.sqrt(b2)
        if(b*b === b2) {
            console.log(`a: ${a}, b: ${b}, c: ${c}`)
        }
        a++
    }
}
pytha(100)
```