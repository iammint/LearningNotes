# DAY41 Find if there is a Cycle of a Linked List
Leetcode 141
1. O(N) 哈希表储存所有node，如果有重复的node，则组成cycle
```js
var hasCycle = function(head) {
    let visit = new Set() 
    while(head != null) {
    if(visit.has(head)) {
        return true
    } 
    visit.add(head)
    head = head.next
    }
    return false
};
```


2. O(1) 利用slow，fast指针，如果slow和fast重叠，则组成cycle  
```js
var hasCycle = function(head) {
    let slow = head, fast = head
    while(fast !== null && fast.next !== null) {
        slow = slow.next
        fast = fast.next.next
        if(slow === fast) {
            return true
        }
    }
    return false
};
```

