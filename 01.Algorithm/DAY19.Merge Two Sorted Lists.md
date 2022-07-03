# DAY19 Merge Two Sorted Lists
合并两个有序的数组

不改变原数组
```js
    function merge(a, b) {
      let i = 0, j = 0, la = a.length, lb = b.length
      let c = []
      while(i<la && j<lb) {
        if(a[i]<=b[j]) {
          c.push(a[i])
          i++
        } else {
          c.push(b[j])
          j++
        }
      }
      //如果有一个数组长度较短则会跳出while
      while(i<la) {
        c.push(a[i++])
      }
      while(j<lb) {
        c.push(b[j++])
      }
      return c
    }
    
    console.log(merge([1, 2, 4, 5], [3, 6, 7, 8]))
```

改变原数组

```js
function merge(a, b) {
    let la = a.length, lb = b.length, c = []
    while(la && lb) {
    if(a[0] < b[0]) {
        c.push(a.shift())
    }
    else {
        c.push(b.shift())
    }
    }
    return c.concat(a, b)
}
console.log(merge([1, 2, 4, 5], [3, 6, 7, 8]))
```

