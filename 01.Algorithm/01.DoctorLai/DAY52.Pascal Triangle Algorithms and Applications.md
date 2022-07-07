# DAY52 杨辉三角
![pascalTriangle.png](https://media.haochen.me/pascalTriangle.png)
```js
function pascal(row, colum) {
    if(row === 0 || colum === 0 || row === colum) {
        return 1
    }
    return pascal(row-1, colum) + pascal(row-1, colum-1)
}
//存在大量重复运算
```

```js
var generate = function(numRows) {
    const ret = []
    for(let i=0; i<numRows; i++) {
        const row = new Array(i+1).fill(i)
        for(let j=1; j<(row.length-1); j++) {
            row[j] = ret[i-1][j] + ret[i-1][j-1]
        }
        ret.push(row) 
    }
    return ret
};
```
