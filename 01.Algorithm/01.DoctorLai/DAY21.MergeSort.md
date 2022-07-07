# DAY21 MergeSort
归并排序（Merge sort）是建立在归并操作上的一种有效、稳定的排序算法，该算法是采用分治法(Divide and Conquer）的一个非常典型的应用。 将已有序的子序列合并，得到完全有序的序列；即先使每个子序列有序，再使子序列段间有序。 若将两个有序表合并成一个有序表，称为二路归并。

```js
    function mergeSort(nums) {
      if(nums.length < 2) {
        return nums
      }
      let middle = Math.floor(nums.length/2)
      let left = nums.slice(0, middle)
      let right = nums.slice(middle)
      let sortedLeft = mergeSort(left)
      let sortedRight = mergeSort(right)
      return merge(sortedLeft, sortedRight)
    }
    function merge(left, right) {
      let i=0, j=0
      let ans = []
      while(i<left.length && j<right.length) {
        if(left[i]<right[j]) {
        ans.push(left[i])
        i++
      }
      else{
        ans.push(right[j])
        j++
      }
      }
      if(i<left.length) {
        ans = ans.concat(left.slice(i))
      }
      if(j<right.length) {
        ans = ans.concat(right.slice(j))
      }
      return ans
    }
    console.log(mergeSort([2,0,4,6,7,8,1,9]))
```