## Решение

```typescript
function reverseList(head: ListNode | null): ListNode | null {
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
  // time: O(n)
  // mem: O(1)
  // на каждом шаге curr двигаем по листу на 1 ноду вперед,
  // а prev - поддерживает массив в котором будет ответ, т е

  // если есть изначально массив
  // 1 -> 2 -> 3 -> 4 -> 5 -> None

  // то через несколько шагов он будет таким
  // None <- 1 <- 2      3 -> 4 -> 5 -> None
  //            prev    curr

  // таким образом в prev мы получим конечный ответ
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
```

**Оценка по времени:** O(n)

**Оценка по памяти:** O(1)

**Описание решения:**

https://kinescope.io/ikJozq5g6YAEmbRQXrRuNn

1. В `prev` будем хранить новые связи нашего списка, а в `current` двигаться на каждой итерации на один шаг

2. `temp` нужна для того, чтобы когда мы подвинем `current` мы могли связать предыдущий `current` c `prev`
