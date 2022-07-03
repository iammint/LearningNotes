# DAY5 Queue
> Queue is a Data Strcuture.
>
> First In First Out

```js
peek:
stack: arr[-1];
queue: arr[0];
```

## Queue
```js
function sqr(nums) {
    ans = [];
    while(nums.length > 0) {
    x= nums.shift();
    x **= 2;
    ans.push(x);
    }
    return ans;
}
//nums=[1, 2, 3, 4, 5, 6, 7]
//ans=[1, 4, 9, 16, 25, 36, 49]
```

## Stack
```js
function sqr(nums) {
    ans = [];
    while(nums.length > 0) {
    x= nums.pop();
    x **= 2;
    ans.push(x);
    }
    return ans;
}
//nums=[1, 2, 3, 4, 5, 6, 7]
//ans=[49, 36, 25, 16, 9, 4, 1]
```
