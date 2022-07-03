# DAY53 Compute the Kth Last Node and Length of a Linked List
## Leetcode 剑指 Offer 22. 链表中倒数第k个节点
方法一：通过计算链表长度与k的关系
```js
var getKthFromEnd = function(head, k) {
    //链表中倒数第K个节点是正数第length-k个节点
    let dummy = new ListNode(0)
    dummy.next = head
    let pointer = dummy, length = 0
    while(pointer.next) {
        length++
        pointer = pointer.next
    }
    for(let i=0; i<length-k; i++) {
        dummy = dummy.next
    }
    return dummy.next
};
```

方法二：维护两个指针
> fast 指针指向链表的第 k + 1 个节点，slow指针指向链表的第一个节点，fast与slow间隔k个节点。两个指针同步向后走，当fast指针指到空时，slow刚好指到倒数第k个节点
```js
var getKthFromEnd = function(head, k) {
    let fast = head, slow = head;
    
    while (fast && k > 0) {
        // [fast, k] = [fast.next, k - 1];
        //fast指向第k+1个节点
        fast = fast.next
        k = k - 1
    }
    while (fast) {
        [fast, slow] = [fast.next, slow.next];
    }
    return slow;
};
```