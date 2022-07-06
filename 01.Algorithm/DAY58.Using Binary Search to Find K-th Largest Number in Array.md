# DAY58 Using Binary Search to Find K-th Largest Number in Array
## Leetcode 1985
Find k-th largest number in Array

```js
var kthLargestNumber = function(nums, k) {
    //第K大的整数，从大到小排列索引第K-1个
    return nums.sort((a, b) => b.length - a.length || b - a )[k - 1]
};
//数字太大的无法相减，因此需要用>大于<小于比较符号来作比较
```

```js
var kthLargestNumber = function(nums, k) {
    //第K大的整数，从大到小排列索引第K-1个
    return nums.sort((a, b) => b.length - a.length || (b > a ? 1 : -1))[k - 1]
};
```

## Using Binary Search
```js
function countEqualOrBig(nums, x) {
    let ans = 0
    for(let i=0; i<nums.length; i++) {
        if(nums[i] >= x) {
            ans++
        }
    }
    return ans
}
function Klargest(nums, k) {
    let left = nums[0], right = nums[0], middle
    for(let i=0; i<nums.length; i++) {
        if(nums[i] < left) {
            left = nums[i]
        }
        if(nums[i] > right) {
            right = nums[i]
        }
    }
    while(left <= right) {
        middle = (left + right)/2
        let x = countEqualOrBig(middle)
        if(x >= k) {
            left = middle + 1
        } else {
            right = middle - 1
        }
    }
    return right
}
```