# DAY39 Linked list 链表
## 链表定义
链表是一个类似于数组的线性结构。但是不同于数组的是，储存在内存中的元素没有特定的位置或者索引。每个元素都是单独的对象（node），包含：数据和pointer指针，pointer指着下个对象

![linkedList.png](https://media.haochen.me/linkedList.png)

一个链表的入口点被称为head，head指着链表的第一个元素。
最后一个元素指着null

空链表的head是一个空引用。

```js
const list = {
    head: {
        value: 6
        next: {
            value: 10                                             
            next: {
                value: 12
                next: {
                    value: 3
                    next: null	
                    }
                }
            }
        }
    }
};
```

## 链表的优势
Nodes can easily be removed or added from a linked list without reorganizing the entire data structure. This is one advantage it has over arrays.

## 链表的劣势
1. Search operations are slow in linked lists. Unlike arrays, random access of data elements is not allowed. Nodes are accessed sequentially starting from the first node.
2. It uses more memory than arrays because of the storage of the pointers.

## 链表的种类
- Singly Linked Lists
  - Each node contains only one pointer to the next node.
- Doubly Linked Lists
  - Each node contains two pointers, a pointer to the next node and a pointer to the previous node.
- Circular Linked Lists
  - Circular linked lists are a variation of a linked list in which the last node points to the first node or any other node before it, thereby forming a loop.


## 实现链表的node
```js
class ListNode {
    constructor(data) {
        this.data = data
        this.next = null                
    }
}
```


## 实现链表
```js
class LinkedList {
    constructor(head = null) {
        this.head = head
    }
}
//创建node1和node2
let node1 = new ListNode(2)
let node2 = new ListNode(5)
node1.next = node2
//创建一个包含node1的链表
let list = new LinkedList(node1)
//获取节点的值
console.log(list.head.next.data) //returns 5
```

## 链表的方法
1. size()
2. clear()
3. getLast()
4. getFirst()



## leetcode 21 合并两个有序链表
声明一个新的节点，用pointer来记录链表的顺序
```js
var mergeTwoLists = function(list1, list2) {
     if(!list1) {
         return list2
     }   
     if(!list2) {
         return list1
     }
     const dummy = new ListNode()
     let p = dummy
    while(list1 && list2) {
        if(list1.val < list2.val) {
            p.next = list1
            list1 = list1.next
        }
        else {
            p.next = list2
            list2 = list2.next
        }
        p = p.next
    }
    if(list1) {
        p.next = list1
    }
    if(list2) {
        p.next = list2
    }
    return dummy.next
};
```