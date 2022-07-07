# DAY9 Two Sum两数之和
在一个数字数组中找到两数值的和等于某值
### 复杂度最高的方法：
```js
let twoSum = function(nums, target) {
    for(let i=0; i<nums.length; i++) {
        for(let j=i+1; j<nums.length; j++) {
            if(nums[i]+nums[j]===target) {
                return [i, j];
                j--;
            }
        }
    }
};
```
### 简便方法：
```js
let twoSum = function(nums, target) {
    nums = nums.sort((a,b)=>a-b);
    let left = 0;
    let right = nums.length - 1;
    for(let i=0; i<nums.length; i++) {
    if(nums[left]+nums[right]===target) {
        return [left, right];
    } else if(nums[left]+nums[right]>target) {
        right -= 1;
    } else {
        left += 1;
    }
    }
};
```