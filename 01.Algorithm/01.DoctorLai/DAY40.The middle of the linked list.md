# DAY40 链表的中间结点
leetcode 876
只要快指针不是最后一个节点，就可以继续往后
```js
var middleNode = function(head) {
    let slow = head, fast = head
    while(fast !== null && fast.next !== null) {
        slow = slow.next
        fast = fast.next.next
    }
    return slow
};
```