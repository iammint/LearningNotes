# DAY13 Greatest Common Divisor and Least Common Multiples
## Greatest Common Divisor
求a与b的最大公约数和最小公倍数
```js
function GCD(a, b) {
    while(b > 0) {
        [a, b] = [b, a % b];
    }
    return a;
}
function LCM(a, b) {
    return a*b/GCD(a,b);
}
```
