# DAY48 Remove Nodes from a Linked List

## leetcode 203
![leetcode203.png](https://media.haochen.me/leetcode203.png)
- 迭代
```js
var removeElements = function(head, val) {
    const dummy = new ListNode(0)
    dummy.next = head
    let pointer = dummy
    while(pointer.next != null) {
        if(pointer.next.val === val) {
            pointer.next = pointer.next.next
        } else {
            pointer = pointer.next
        }
    }
    return dummy.next
};
```
- 递归
```js
let removeElements = function(head, val) {
    if(head == null) {
        return head
    }
    head.next = removeElements(head.next,  val)
    return head.val === val ? head.next : head
}
```