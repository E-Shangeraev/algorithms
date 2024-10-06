## Решение

```typescript
function maxDistToClosest(seats: number[]): number {
  let left = 0;
  let right = 0;
  let maxDistance = 0;

  while (left < seats.length) {
    while (right + 1 < seats.length && seats[right + 1] === seats[right]) {
      right++;
    }

    if (seats[right] === 0) {
      if (left === 0 || right === seats.length - 1) {
        maxDistance = Math.max(maxDistance, right - left + 1);
      } else {
        maxDistance = Math.max(maxDistance, Math.floor((right - left) / 2 + 1));
      }
    }

    left = right + 1;
    right = right + 1;
  }

  return maxDistance;
}
```

## Эталонное решение

```javascript
/**
 * @param {number[]} seats
 * @return {number}
 */
const maxDistToClosest = function (seats) {
  let l = 0;
  let r = 0;
  let result = 0;
  while (l < seats.length) {
    // before
    // l
    // 1 1 1 1 0 0 1 1
    // r

    // бежим правым указателем пока в интервале [l, r]
    // находятся все последовательные числа
    while (r + 1 < seats.length && seats[r] === seats[r + 1]) {
      r += 1;
    }
    // after
    // l
    // 1 1 1 1 0 0 1 1
    //       r

    // обновляем ответ только если в палавающем окне были 0-ли
    if (seats[r] === 0) {
      // если 0 прижат к стенке слева или справа, т. е.
      // 1 0 0 0
      //   l   r

      // 0 0 0 1
      // l   r
      // то свободных мест будет r - l + 1 т к посадим в самый край
      if (l === 0 || r === seats.length - 1) {
        result = Math.max(result, r - l + 1);
      }
      // в данном случае окно распологается между 1-ами:
      // 1 0 0 0 1
      //   l   r
      // поэтому находим число мест по формуле (r - l + 2) // 2
      else {
        result = Math.max(result, Math.floor((r - l + 2) / 2));
      }
    }

    // интервалы не пересекаются, поэтому сдвигаем
    // на r + 1 - именно отсюда будет начинаться
    // следующий интервал
    l = r + 1;
    r = r + 1;
  }
  return result;
};
```

**Оценка по времени:** O(n)

**Оценка по памяти:** O(1)

**Описание решения:**

https://kinescope.io/mAzYfZCDmsVwjQqftiVGmy

1. Непересекающиеся окна. Ставим левый и правый указатели в начало массива.

2. Правый указатель двигается если следующий элемент равен текущему.

3. Если вышли из цикла и текущий элемент равен единице - переходим к шагу 4. Если нулю, то нужно проверить два кейса:

- если текущее окно прижато к стене (левой или правой), то формула результата `Math.max(result, right - left + 1)`
- если окно не скраю, то формула `Math.max(maxDistance, Math.floor((right - left) / 2 + 1))`

4. Двигаем оба указателя на `right + 1`.
