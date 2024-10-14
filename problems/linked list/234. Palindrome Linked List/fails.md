Медленный указатель перемещал на 2 шага при поиске середины. Ошибка по невнимательности

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

function findMiddle(head: ListNode | null): ListNode | null {
  let s = head;
  let f = head;

  while (f !== null && f.next !== null) {
    f = f.next.next;
    s = s.next.next;
  }

  return s;
}

function reverseLinkedList(head: ListNode | null): ListNode | null {
  let prev = null;
  let current = head;

  while (current !== null) {
    const temp = current;
    current = current.next;
    temp.next = prev;
    prev = temp;
  }

  return prev;
}

function isPalindrome(head: ListNode | null): boolean {
  const middle = findMiddle(head);
  const rightPart = reverseLinkedList(middle);

  let p1 = head;
  let p2 = rightPart;

  while (p1 !== null && p2 !== null) {
    if (p1.val !== p2.val) {
      return false;
    }

    p1 = p1.next;
    p2 = p2.next;
  }

  return true;
}
```
