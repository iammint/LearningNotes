# DAY29 Binary Tree Traversal 
Inorder中序遍历, Preorder先序遍历, Postorder后序遍历

Inorder => Left, Root, Right.

Preorder => Root, Left, Right.

Post order => Left, Right, Root.
# 中序遍历
> 中序遍历是二叉树遍历的一种，也叫做中根遍历、中序周游。在二叉树中，中序遍历首先遍历左子树，然后访问根结点，最后遍历右子树。

## LeetCode 94 中序遍历
法一：递归recursion
```js
var inorderTraversal = function(root, ans = []) {
    if(!root) return []
    inorderTraversal(root.left, ans)
    ans.push(root.val)
    inorderTraversal(root.right, ans)
    return ans
};
```
法二：迭代
```js
var inorderTraversal = function(root) {

      let stack = []
      let result = []
      while(root || stack.length) {
        while(root) {
          stack.push(root)
          root = root.left
        }
      root = stack.pop()
      result.push(root.val)
      root = root.right
    }
      return result
};
```


## LeetCode 145 后序遍历
```js
var postorderTraversal = function(root, ans = []) {
    if(root === null) return []
    postorderTraversal(root.left, ans)
    postorderTraversal(root.right, ans)
    ans.push(root.val)
    return ans
};
```

## 前序遍历
```js
var postorderTraversal = function(root, ans = []) {
    if(root === null) return []
    ans.push(root.val)
    postorderTraversal(root.left, ans)
    postorderTraversal(root.right, ans)
    return ans
};
```