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

function removeNthFromEnd(head: ListNode | null, n: number): ListNode | null {
  const dummy = new ListNode(0, head);
  let p = dummy;
  let size = 0;
  let curIndex = 0;

  while (head !== null) {
    head = head.next;
    size++;
  }

  while (p !== null) {
    if (curIndex === size - n) {
      p.next = p.next.next;
    }

    p = p.next;
    curIndex++;
  }

  return dummy.next;
}
```

## Эталонное решение

1.

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
 * @param {number} n
 * @return {ListNode}
 */
var removeNthFromEnd = function (head, n) {
  // time:      O(n), где n - длина списка
  // mem(доп):  O(1)
  let dummyNode = new ListNode(0, head);

  let fast = dummyNode;
  for (let i = 0; i < n + 1; i++) {
    fast = fast.next;
  }

  let slow = dummyNode;
  while (fast !== null) {
    slow = slow.next;
    fast = fast.next;
  }

  // удаляем вершину
  slow.next = slow.next.next;

  return dummyNode.next;
};
```

2.

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
 * @param {number} n
 * @return {ListNode}
 */
var removeNthFromEnd = function (head, n) {
  let dummyNode = new ListNode(0, head);

  // находим длину списка с учетом dummyNode
  let length = 0;
  let curr = dummyNode;
  while (curr !== null) {
    curr = curr.next;
    length++;
  }

  // доходим до (n-1)-ой вершины с конца
  curr = dummyNode;
  for (let i = 0; i < length - n - 1; i++) {
    curr = curr.next;
  }

  // удаляем вершину
  curr.next = curr.next.next;

  return dummyNode.next;
};
```

**Оценка по времени:** O(n), где n - длина списка

**Оценка по памяти:** O(1)

**Описание решения:**

https://kinescope.io/5sYGWJitSsNXnu3pQDtR8u

Опишу свое решение.

1. Паттерн Dummy node. Сначала считаю длину списка.

2. Затем снова последовательно иду по списку, считаю индекс. Останавливаемся на том элементе, который перед удаляемым. Его индекс будет равен `(size - n)`.
