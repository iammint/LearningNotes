# DAY10 Inverse Factorials
逆向计算阶乘的两种算法
## 方法一：利用乘（暴力枚举）
```js
    function ReverseFactorial(n) {
      if(n < 1) return -1;
      else if(n === 1) return 1;
      let i = 2;
      let s = 1;
      while(s < n) {
        s *= i;
        i++;
      }
      if(s === n) return i - 1;
      else return -1;
    }
```
## 方法二：利用除（更简便快速）
```js
function ReverseFactorial(n) {
  if(n < 1) return -1;
  else if(n === 1) return 1;
  let i = 2;
  while(n > 1) {
    if(n % i != 0) {
    return -1;
    }
  n /= i;
  i++;
  }
  return i - 1;
}
```






