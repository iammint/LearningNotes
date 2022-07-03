# DAY4 Reversing a List using Stack
## Stack FILO
> Stack is a Data Strcuture.
> 
> First In Last Out

Reversing a list using stack:

```js
function rev(nums) {
  ans = [];
  while(nums.length > 0) {
    let x = nums.pop();
    ans.push(x);
  }
  return ans;
}
```

## leetcode 682
![alt ](../../CSS与img引用/../JavaScript/CSS与img引用/Algorithm/leetcode682.png)
```js
var calPoints = function(ops) {
    //是要将经过规则转换之后的值加入到新的数组中
    let stack = [];
    //要遍历ops
    for(num of ops) {
        switch(num) {
            case "C" :
            //此时未加入新的分数，所以上一个就是stack的最后一个
            stack.pop();
            break;

            case "D" :
            //stack.length-1就是最后一个，索引比长度小1
            stack.push(stack[stack.length - 1]*2);
            break;

            case "+" :
            stack.push(stack[stack.length - 1] + stack[stack.length - 2]);
            break;

            default:
            //注意次数必须向新数组中加入数字
            stack.push(Number(num));
            break;
        }
    }
    return stack.reduce((a,b) => a + b);
}
```
