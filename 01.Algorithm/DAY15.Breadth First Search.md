# DAY15 Revisit BFS Algorithm via Jump Game
# 利用BFS(Breadth First Search)解决Jump Game问题

## 深度优先遍历DFS
该方法是以纵向的维度对DOM树进行遍历，从第一个DOM节点开始，一直遍历其子节点，直到它的所有子节点都被遍历完毕后再遍历它的兄弟节点

## 广度优先遍历BFS
该方法是以横向的维度对DOM树进行遍历，从该节点的第一个子节点开始，遍历其所有的兄弟节点，再遍历第一个节点的子节点，完成该遍历后，暂时不深入，开始遍历其兄弟节点的子节点。

例如:[2,0,3,1,3,4] 以 1 为起点，0 为目标，如果能跳跃到目标位置。可以左右跳，当前元素代表你在该位置可以跳跃的最大长度
![alt ](../CSS%E4%B8%8Eimg%E5%BC%95%E7%94%A8/Algorithm/BFS%E8%B7%B3%E8%B7%83game.png)

```js
function BFS(nums, start, target) {
    //传入一个数组，利用BFS如果可以找到target则返回true，否则返回false
  let queue = [start]
  let seen = new Set()
  while (queue.length > 0) {
    const element = queue.shift();
    seen.add(element);
    if (nums[element] === target) {
      return true;
    }
    for (const i of [-1, 1]) {
      const next = element + i*nums[element]
      if (next >= 0 && next <= nums.length - 1 && !seen.has(next)) {
        queue.push(next);
      }
    }
  }
  return false
}
```

## Leetcode55
![alt ](../CSS与img引用/Algorithm/leetcode55.png)
这题我们可以维护一个最大能到达的 index 值，遍历数组并与当前下标进行比较然后更新最大 index 值。

核心思想：如果能到达一个值，则这个值左侧的值也都能到达。
```js
function canJump(nums) {
  let k = 0
  for (let i = 0; i < nums.length; i++) {
    if (k < i) return false
    k = Math.max(k, i + nums[i])
  }
  return true
}
```


```js
// breadth first search
    function BFS() {
      let currentNode = this.root
      let queue = []
      let result = []
      queue.push(currentNode)

      while(queue.length) {
        currentNode = queue.shift()
        result.push(currentNode)
        if(currentNode.left) {
          queue.push(currentNode.left)
        }
        if(currentNode.right) {
          queue.push(currentNode.right)
        }
      }
      return result
    }
```