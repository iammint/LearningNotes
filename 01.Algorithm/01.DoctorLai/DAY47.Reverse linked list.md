# DAY47 Reverse linked list
## leetcode 24 反转链表
```js
var reverseList = function(head) {
    if(!head || !head.next) {
        return head
    }
    //prev必须是null，不能从head开头否则会形成cycle
    let prev = null
    let curr = head
    while(curr) {
        //必须使用一个变量把进入while语句之前的curr.next存起来，否则curr.next变成了prev，进入死循环
        const next = curr.next
        curr.next = prev
        prev = curr
        curr = next
    }
    return prev
};
```



