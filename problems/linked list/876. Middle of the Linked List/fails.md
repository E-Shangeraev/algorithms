Ошибка в перемещении указателей –– они всегда стоят на месте

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

function middleNode(head: ListNode | null): ListNode | null {
  let s = head;
  let f = head;

  while (f !== null && f.next !== null) {
    f = head.next.next;
    s = head.next;
  }

  return s;
}
```
