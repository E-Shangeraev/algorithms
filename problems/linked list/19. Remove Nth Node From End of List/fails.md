Наивно предположил, что все значения узлов будут строго в возрастающем порядке: 1, 2, 3, 4 и тд. Использовал значения, а не индексы

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

function removeNthFromEnd(head: ListNode | null, n: number): ListNode | null {
  const dummy = new ListNode(0, head);
  let p = dummy;
  let size = 0;

  while (head !== null) {
    head = head.next;
    size++;
  }

  while (p !== null) {
    if (p.val === size - n) {
      p.next = p.next.next;
    }

    p = p.next;
  }

  return dummy.next;
}
```
