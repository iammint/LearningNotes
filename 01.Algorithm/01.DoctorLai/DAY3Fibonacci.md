## DAY3 Fibonacci Number - Recursion

> 斐波那契数是以递归的方法来定义：
> 
> F(0)=0
> F(1)=1
> F(n)=F(n-1)+F(n-2)


用文字来说，就是斐波那契数列由0和1开始，之后的斐波那契数就是由之前的两数相加而得出。首几个斐波那契数是：

1、 1、 2、 3、 5、 8、 13、 21、 34、 55、 89、 144、 233、 377、 610、 987……


### Non Recursive Version
```js
function fib(n) {
    if(n<3) {
        return 1;
    }
    let prev = 1;
    let curr = 1;
    for(let i=2; i<n; i++) {
        const next = curr + prev;
        prev = curr;
        curr = next;
    }
    return curr;
}
```

### 普通递归
```js
function fib(n) {
    if(n===0) {
        return 0;
    } else if(n===1) {
        return 1;
    }
    return fib(n-1) + fib(n-2);
}
//显然存在重复运算，我们可以将求过的值缓存起来
```

### 改进递归 —— 把前两位数字做成参数避免重复计算
```js
function fibonacci(n) {
    function fib(n, v1, v2) {
        if (n == 1)
            return v1;
        if (n == 2)
            return v2;
        else
            return fib(n - 1, v2, v1 + v2)
    }
    return fib(n, 1, 1)
}
```

### for循环+解构赋值
```js
function fib(n) {
    let a = 0;
    let b = 1;
    for(let i=0; i<n; i++) {
        [a, b] = [b, a+b];
    }
    return a;
}
```