# DAY33 Sum of first even numbers
## 利用奇偶和减去奇数和即可得到偶数和

N代表的是第几个奇数/偶数，因此奇偶数和是前2N个数字的和

前N个奇数和：N*N

前2N个数的和(先奇后偶)：2N*(2N+1)/2

经过相减，前N个偶数和：N*N+N

# Math Induction 验证
f(N)表示前N个偶数的和

    f(N)=N*N+N

    f(1)=1

    f(k)=k*k+k

    f(k+1)=f(k)+第k+1个偶数

          =k*k+k + 2(k+1)

          =(k+1)*(k+1)*+(k+1)


复杂度O(N)
```js
function sumOfEven(n) {
    let ans = 0
    for(let i=2; i<=2*n+1; i=i+2) {
        ans += i
    }
    return ans
}
console.log(sumOfEven(5))
```
复杂度O(1)
```js
function sumOfEven(n) {
    return n*n+n
}
```