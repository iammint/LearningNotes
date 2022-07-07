# DAY38 Prefix Sum Algorithm to Compute the Interval Sums 
通过前缀和来计算区间的和

```js
function prefixComputeIntervalSums(nums, start, end) {
    let sum = 0
    let prefix = [0]
    for(const i of nums) {
        sum += i
        prefix.push(sum)
    }
    return prefix(end + 1) - prefix(start)
}
```