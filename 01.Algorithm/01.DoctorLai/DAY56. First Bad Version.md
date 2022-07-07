# DAY56  First Bad Version
## Leetcode 278
![Leetcode278.png](https://media.haochen.me/Leetcode278.png)
```js
var solution = function(isBadVersion) {
    return function(n) {
        let left = 1, right = n
        let middle
        while(left <= right) {
            middle = parseInt((left+right)/2)
            if(isBadVersion(middle)) {
                if(!isBadVersion(middle-1)) {
                    return middle
                }
                right = middle - 1
            } else {
                left = middle + 1
            }
        }
        return middle
    };
};
```
