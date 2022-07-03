# DAY55 Transpose a Matrix 矩阵转置
eg: [[1, 2, 3], [4, 5, 6]]   2×3的矩阵
![transposeMatrix.png](https://media.haochen.me/transposeMatrix.png)

矩阵转置：row -> column, column -> row
## Leetcode 867
先根据row和column创建出ans的数组模型，再遍历两次填满
```js
var transpose = function(matrix) {
    let row = matrix.length //2
    let column = matrix[0].length //3
    let ans = new Array(column).fill(0).map(item => 
        new Array(row).fill(0))
    for(let i=0; i<row; i++) {
        for(let j=0; j<column; j++) {
            ans[j][i] = matrix[i][j]
        }
    }
    return ans
};
```

