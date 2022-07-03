# DAY32 Sum of the first odd numbers: Math Induction

f(n) = n**2

f(1) = 1

f(k) = k**2

f(k+1) = f(k)+第k+1个奇数 = k**2 + 2k+1 = (k+1)**2

```js
function sumOfOdd(n) {
    return n**2
}
```