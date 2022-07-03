# DAY2 From Linear Search to binary search

## 线性搜索（Brute Force）
> 在计算机科学中，线性搜索或顺序搜索是一种寻找某一特定值的搜索算法，指按一定的顺序检查数组中每一个元素，直到找到所要寻找的特定值为止。是最简单的一种搜索算法。 
## 二分搜查
> 是一种在有序数组中查找某一特定元素的搜索算法。搜索过程从数组的**中间元素**开始，如果中间元素正好是要查找的元素，则搜索过程结束；如果某一特定元素大于或者小于中间元素，则在数组大于或小于中间元素的那一半中查找，而且跟开始一样从中间元素开始比较。如果在某一步骤数组为空，则代表找不到。这种搜索算法每一次比较都使搜索范围缩小一半。
> - 除非输入数据数量很少，否则二分查找算法比线性搜索更快，**但数组必须事先被排序**。


### Linear Search:
```js
function sqrt(n):
    for(let i=0; i<n; i++) {
    if i * i == n:
        return i
    }
```
The complexity is O(N) - linear time.

### Binary search implementation:
```py
    def sqrt(n):
    left, right = 0, n
    while left <= right:
      mid = (left + right) // 2
      if mid * mid == n:
         return mid
      if mid * mid &gt;= n:
         right = mid - 1
      else:
         left = mid + 1
```
The complexity is O(logN)

### Linear Search:
```js
const arr = [0, 1, 2, 3, 4, 5, 6, 7, 8]
function search(value, arr) {
    for(let i=0; i<arr.length; i++) {
        if(value == arr[i]) {
            return i;
        } return -1;
    }
}
```

### Binary search implementation:
## LeetCode
![alt 704](../CSS与img引用/Algorithm/DAY2Binary%20Search.png)
```js
function Binary(target, nums) {
    let lower = 0;
    let upper = (nums.length - 1);
    while(lower <= upper) {

        console.log("try");

        //获取nums数量的一半
        const middle = lower + Math.floor((upper - lower)/2);
        // Math.floor((upper - lower)/2)获取的是数量而不是索引，
        //所以要从第一个索引开始加，才是中间位置

        if(target === nums[middle]) {
            return middle;
        }

        else if(target < nums[middle]) {
            upper = middle - 1;
        }

        else {
            lower = middle + 1;
        }
    }
    return -1;
}

console.log(Binary(7, [1, 2, 8, 9, 5, 0, 4, 7, 2, 6]));
```


