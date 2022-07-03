# DAY34 Count the Number of Nodes in Binary Tree using DFS and BFS
## Leetcode 222
```js
// BFS
function countNodes(root) {
  if (root == null) {
    return 0
  }
  let queue = [root]
  let ans = 0
  while (queue.length) {
    let node = queue.shift()
    ans += 1
    if (node.left != null) {
      queue.push(node.left)
    }
    if (node.right != null) {
      queue.push(node.right)
    }
  }
  return ans
}

// DFS
function countNodes(root) {
  if (root == null) {
    return 0
  }
  return 1 + countNodes(root.left) + countNodes(root.right)
}
```