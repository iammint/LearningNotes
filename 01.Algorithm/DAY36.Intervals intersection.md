# DAY36 Intervals intersection
> (0,2)与(1,3)的交集是(1,2)
```js
  function intersection(intervalArr) {
    //intervalArr eg:[[0,2],[1,3]]
    if(intervalArr.length === 0) {
      return []
    }
    let left1 = intervalArr[0][0]
    let right1 = intervalArr[0][1]
    let left, right
    for(let i in intervalArr) {
      left = Math.max(left1, intervalArr[i][0])
      right = Math.min(right1, intervalArr[i][1])
    }
    if(left > right) {
      return []
    }
    return [left, right]
  }
  intersection([[0,2],[1,3]])
```


## Leetcode 986
![alt ](../CSS%E4%B8%8Eimg%E5%BC%95%E7%94%A8/Algorithm/leetcode986.png)
输入：

firstList = [[0,2],[5,10],[13,23],[24,25]], secondList = [[1,5],[8,12],[15,24],[25,26]]

输出：

[[1,2],[5,5],[8,10],[15,23],[24,24],[25,25]]
```js
let intervalIntersection = function(firstList, secondList) {
    if(firstList.length === 0 || secondList.length === 0) {
        return []
    }
    let ans = []
    let i=0, j=0
    while(i < firstList.length && j < secondList.length) {
        let left = Math.max(firstList[i][0], secondList[j][0])
        let right = Math.min(firstList[i][1], secondList[j][1])
        if(left <= right) {
            ans.push([left, right])
        }
        //哪个右区间元素较小，就向前移动一位
        //下一个右区间再作比较
        if(firstList[i][1] < secondList[j][1]) {
            i++
        } else {
            j++
        }
    }
    return ans
};
```