# DAY1 Recursion

## What is Recursion?
>在数学和计算机科学中，递归指由一种（或多种）简单的基本情况定义的一类对象或方法，并规定其他所有情况都能被还原为其基本情况。递归是指在函数的定义中使用函数自身的方法。

> - 函数不断地在调用自己，直到找到终点，把结果沿着原来的路线进行传递，最终回归到起点。

```py
        def f(n):
        if n==1 return 1
        return n*f(n-1)
```

### 递归逐乘
``` js
        function multiply(arr, n) {
            if(n==1) {
                return 1;
            } return multiply(arr, n-1)*arr[n-1];
        }
```
### 递归逐加
``` js
        function sum(arr, n) {
            if(n==0) {
                return 0;
            } return sum(arr, n-1) + arr[n-1];
        }
```
  
## 面试题
#### 1个细胞每1个小时分裂一次，生命周期是3小时，求n小时后容器内有多少个细胞？
![DAY1.png](https://media.haochen.me/DAY1.png)
```js
function cells(n) {
    function cell3(n) {
        if(n===0 || n===1) {
            return 0;
        }
        return cell2(n-1);
    }
    function cell2(n) {
        if(n===0) {
            return 0;
        }
        return cell1(n-1);
    }

    function cell1(n) {
        if(n===0) {
            return 1;
        }
        return cell1(n-1) + cell2(n-1) + cell3(n-1);
    }

        return cell1(n) + cell2(n) + cell3(n);
    }
    console.log(cells(4));
```
<font color=red>
  要能找到起点：每个递归函数里都要写出口，出口是递归函数的关键</font>