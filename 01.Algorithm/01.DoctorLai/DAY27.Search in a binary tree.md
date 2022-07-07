# DAY27 Search in a binary tree
二叉树搜查
### leetcode 257
![alt ](../CSS%E4%B8%8Eimg%E5%BC%95%E7%94%A8/Algorithm/leetcode257.png)
```js
var binaryTreePaths = function(root) {
      if(!root) return []
      const result = []
      function findPath(node, currentPath) {
        currentPath += node.val.toString()
        if(!node.left && !node.right) {
          result.push(currentPath)
        }
        if(node.left) {
          findPath(node.left, currentPath + "->")
        }
        if(node.right) {
          findPath(node.right, currentPath + "->")
        }
      }
      findPath(root, "")
      return result
};
```
### leetcode 98
![leetcode98.png](https://media.haochen.me/leetcode98.png)
```js
const helper = (root, lower, upper) => {
    if (root === null) {
        return true;
    }
    if (root.val <= lower || root.val >= upper) {
        return false;
    }
    return helper(root.left, lower, root.val) && helper(root.right, root.val, upper);
}
var isValidBST = function(root) {
    return helper(root, -Infinity, Infinity);
};

```