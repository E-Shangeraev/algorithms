## Решение

```typescript
/**
 * Definition for singly-linked list.
 * class ListNode {
 *     val: number
 *     next: ListNode | null
 *     constructor(val?: number, next?: ListNode | null) {
 *         this.val = (val===undefined ? 0 : val)
 *         this.next = (next===undefined ? null : next)
 *     }
 * }
 */

function mergeTwoLists(list1: ListNode | null, list2: ListNode | null): ListNode | null {
  const dummy = new ListNode(0);
  let p = dummy;
  let p1 = list1;
  let p2 = list2;

  while (p1 !== null && p2 !== null) {
    if (p1.val <= p2.val) {
      p.next = p1;
      p1 = p1.next;
    } else {
      p.next = p2;
      p2 = p2.next;
    }

    p = p.next;
  }

  if (p1 === null) {
    p.next = p2;
  }

  if (p2 === null) {
    p.next = p1;
  }

  return dummy.next;
}
```

## Эталонное решение

```javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} list1
 * @param {ListNode} list2
 * @return {ListNode}
 */
var mergeTwoLists = function (list1, list2) {
  const getVal = node => {
    if (node === null) {
      return Infinity;
    }
    return node.val;
  };
  let curr = new ListNode();
  let stab = curr;
  while (list1 !== null || list2 !== null) {
    if (getVal(list1) < getVal(list2)) {
      curr.next = list1;
      list1 = list1.next;
    } else {
      curr.next = list2;
      list2 = list2.next;
    }
    curr = curr.next;
  }
  return stab.next;
};
```

**Оценка по времени:** O(n + m)

**Оценка по памяти:** O(1)

**Описание решения:**

https://leetcode.com/problems/merge-two-sorted-lists/

1. Паттерн Dummy node. Создаем дамми, куда будем крепить результирующий список

2. Пробегаемся по циклу и выполняем проверку: какое значение меньше, то и прикрепляемz
