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

function middleNode(head: ListNode | null): ListNode | null {
  let s = head;
  let f = head;

  while (f !== null && f.next !== null) {
    f = f.next.next;
    s = s.next;
  }

  return s;
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
 * @param {ListNode} head
 * @return {ListNode}
 */
var middleNode = function (head) {
  // time: O(n)
  // mem (дополнительная): O(1)
  // изначально ставим slow и fast на голову
  let slow = head; // будем двигать на 1 вперед
  let fast = head; // будем двигать на 2 вперед
  // продолжаем сдвигать до тех пор пока fast and fast.next
  // советую нарисовать пару примеров и самому посмотреть что это работает
  // если непонятно почему это работает
  while (fast !== null && fast.next !== null) {
    slow = slow.next;
    fast = fast.next.next;
  }
  return slow;
};
```

sdfsd

**Оценка по времени:** O(n)

**Оценка по памяти:** O(1)

**Описание решения:**

https://kinescope.io/0PoMU1doCUdbacBDkUXnxs

Паттерн "Быстрый и медленный указатели". Быстрый двигается на 2 шага, медленный на 1 при выполнении условия, что быстрый не указывает на `null` и следующий за ним тоже не `null`
