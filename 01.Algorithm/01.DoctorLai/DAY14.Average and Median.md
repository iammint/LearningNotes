# DAY14 Average and Median
## 平均数
```js
    function average(nums) {
        let sum = nums.reduce((a,b)=>a+b);
        return sum/nums.length;
    }
```
## 中位数
```js
function median(nums) {
    let sortedNums = nums.sort((a,b)=>a-b);
    console.log(sortedNums);
    let size = sortedNums.length;
    if(size % 2 === 0) {
        let result = sortedNums[size/2 - 1] + sortedNums[(size/2)];
        return result/2;
    }
    else{
        return sortedNums[parseInt(size/2)];
    }
}
console.log(median([1,5,8,3,9,2,6]));
```