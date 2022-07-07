# DAY54 Compute the Power x^n Function
## Leetcode 50
Brute Force
```js
function pow(x, n) {
    if(x === 1 || n === 0) {
        return 1
    }
    if(x === 0) {
        return 0
    }
    if(n < 0) {
        [x, n] = [1/x, -n]
    }
    let ans = 1
    for(let i=0; i<n; i++) {
        ans *= x
    }
    return ans
}
```

### 法一 递归recursive
```js
function pow(x, n) {
    if(x === 1 || n === 0) {
        return 1
    }
    if(x === 0) {
        return 0
    }
    if(n < 0) {
        [x, n] = [1/x, -n]
    }
    if(n % 2 != 0) { 
        return x*pow(x, n-1) 
    }
    //n为偶数时降低复杂度，2^100 = 2^50 * 2^50
    let y = pow(x, n / 2)
    return y*y
}
```

### 法二 迭代iterative
```js
function pow(x, n) {
    if(x === 1 || n === 0) {
        return 1
    }
    if(x === 0) {
        return 0
    }
    if(n < 0) {
        [x, n] = [1/x, -n]
    }
    let ans = 1
    ❓不会
}
```

