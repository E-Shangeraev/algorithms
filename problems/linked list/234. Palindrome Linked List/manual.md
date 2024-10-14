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

function findMiddle(head: ListNode | null): ListNode | null {
  let s = head;
  let f = head;

  while (f !== null && f.next !== null) {
    f = f.next.next;
    s = s.next;
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

  while (p2 !== null) {
    if (p1.val !== p2.val) {
      return false;
    }

    p1 = p1.next;
    p2 = p2.next;
  }

  return true;
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
var reverseList = function (head) {
  // in:  1 -> 2 -> 3 -> None
  // out: 3 -> 2 -> 1 -> None
  // time: O(n)
  // mem: O(1)
  let prev = null;
  let curr = head;
  while (curr !== null) {
    let tmp = curr;
    curr = curr.next;
    tmp.next = prev;
    prev = tmp;
  }
  return prev;
};

// in:     1  ->  2  ->  3
// out:          mid

// in:     1  ->  2  ->  3  ->  4
// out:                 mid

// time: O(n)
// mem: O(1)
var middleNode = function (head) {
  // изначально ставим slow и fast на голову
  let slow = head; // будем двигать на 1 вперед
  let fast = head; // будем двигать на 2 вперед

  while (fast !== null && fast.next !== null) {
    slow = slow.next;
    fast = fast.next.next;
  }
  return slow;
};

// time: O(n)
// mem: O(1)
var isPalindrome = function (head) {
  let firstHalfEndNode = middleNode(head);
  let secondHalfBeginNode = reverseList(firstHalfEndNode);

  let p1 = head;
  let p2 = secondHalfBeginNode;
  // тут важно понимать как будет выглядеть связный список после манипуляций c поворотом

  //      p1            p2
  // in:  1  ->  2  ->  3
  // out: 1  ->  2  <-  3
  //            /
  //     None <|
  // т е из "2" идет в None

  //      p1                   p2
  // in:  1  ->  2  ->  3  ->  4
  // out: 1  ->  2  <-  3  <-  4
  //                   /
  //            None <|

  // теперь очевидно, что мы должны сравнивать значения в
  // нодах p1 и p2 пока p2 не станет None
  while (p2 !== null && p1 !== null) {
    if (p1.val !== p2.val) {
      return false;
    }
    p1 = p1.next;
    p2 = p2.next;
  }
  // по желанию можно вернуть список в изначальное состояние
  return true;
};
```

**Оценка по времени:** O(n)

**Оценка по памяти:** O(1)

**Описание решения:**

https://kinescope.io/bFfUgWxXRCEKjYFu6tgdLx

1. Ищем середину списка

2. Разворачиваем вторую половину списка

3. Ставим по указателю на первую и вторую половины списка и сравниваем их значения в цикле
