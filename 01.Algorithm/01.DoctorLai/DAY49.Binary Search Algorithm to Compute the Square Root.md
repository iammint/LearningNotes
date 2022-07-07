# DAY49 Binary Search Algorithm to Compute the Square Root
## leetcode 69
```js
var mySqrt = function(x) {
    if(x === 1) {
        return 1
    }
    let low = 0, middle = 0, high = x
    let curr = 0
  while (Math.abs(curr - x) > 1e-8) {
    middle = Math.floor((low + high) / 2)
    curr = middle * middle
    if (curr < x) {
      low = middle
    } else {
      high = middle
    }
  }
  return Math.floor(middle) // toFixed()
}
```