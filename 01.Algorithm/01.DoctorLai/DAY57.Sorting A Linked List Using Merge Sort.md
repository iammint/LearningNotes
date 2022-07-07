# DAY57 Sorting a Linked List using Merge Sort (Divide and Conquer)
1. 找到链表的中点，以中点为分界，将链表拆分成两个子链表。寻找链表的中点可以使用快慢指针的做法，快指针每次移动 22 步，慢指针每次移动 11 步，当快指针到达链表末尾时，慢指针指向的链表节点即为链表的中点。

2. 对两个子链表分别排序。

将两个排序后的子链表合并，得到完整的排序后的链表。可以使用「21. 合并两个有序链表」的做法，将两个有序的子链表进行合并。

```js
//找到中间节点并且断开成两个链表
function breakMid(head) {
    if(head == null || head.next == null) return head
    let fast = head, slow = head, prev = null
    while(fast && fast.next) {
        fast = fast.next.next
        prev = slow
        slow = slow.next
    }
    prev.next = null
    return slow
}
//对两个链表分别排序并且合并
function sort(head) {
    if(head == null || head.next == null) return head
    let lower = sort(head)
    let upper = sort(breakMid(head))
    return merge(lower, upper)
}
👇
function sortList(head) {
    if (!head || !head.next) {
      return head
    }
    let fast = head, slow = head, prev = null
    while(fast && fast.next) {
        fast = fast.next.next
        prev = slow
        slow = slow.next
    }
    prev.next = null
    let sortedLeft = sortList(head)
    let sortedRight = sortList(slow)
    return merge(sortedLeft, sortedRight)
  }

//合并两个有序链表
function merge(a, b) {
    if(!a) return b
    if(!b) return a
    const dummy = new ListNode(0)
    let pointer = dummy
    while(a && b) {
        if(a.val < b.val) {
            pointer.next = a
            a = a.next
        } else {
            pointer.next = b
            b = b.next
        }
        pointer = pointer.next
    }
    if(a!=null) {
        pointer.next = a
    }
    if(b!=null) {
        pointer.next = b
    }
    return dummy.next
}

```