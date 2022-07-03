# DAY20 Quick Sort
##  快排
快排是一种运用分治(divide and conquer )思想的排序算法,平均时间复杂度O(nlogn),最大时间复杂度O(n^2)。
1. 分区

从数组中任意选择一个“基准”，将所有比基准小的元素放在基准前面，所有比基准大的元素放在基准后面

2. 递归

递归地对基准前后的子数组进行分区

```js
    function quickSort(arr) {
      if(arr.length < 2) {
        return arr
      }
      let left = []
      let right = []
      let pivot = arr[arr.length - 1]
      while(arr.length > 1) {
        if(arr[0] < pivot) {
          left.push(arr.shift())
        }
        else {
          right.push(arr.shift())
        }
      }
      return [...quickSort(left), pivot, ...quickSort(right)]
    }
    console.log(quickSort([2,3,4,5,7,8,1,9]))
```
