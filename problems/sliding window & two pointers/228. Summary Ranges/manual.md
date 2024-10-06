## Решение

```typescript
function summaryRanges(nums: number[]): string[] {
  let left = 0;
  let right = 0;
  const result: string[] = [];

  while (left < nums.length) {
    while (right < nums.length && nums[right] + 1 === nums[right + 1]) {
      right++;
    }

    if (left === right) {
      result.push(`${nums[left]}`);
    } else {
      result.push(`${nums[left]}->${nums[right]}`);
    }

    left = right + 1;
    right = right + 1;
  }

  return result;
}
```

## Эталонное решение

```javascript
/**
 * @param {number[]} nums
 * @return {string[]}
 */
const summaryRanges = function (nums) {
  let l = 0;
  let r = 0;
  let result = [];
  while (l < nums.length) {
    // before
    // l
    // 1 2 3 5 7 8
    // r

    // бежим правым указателем пока в интервале [l, r]
    // находятся все последовательные числа
    while (r + 1 < nums.length && nums[r] + 1 === nums[r + 1]) {
      r += 1;
    }
    // after
    // l
    // 1 2 3 5 7 8
    //     r
    // бежим правым указателем

    // добавлем в ответ
    if (r !== l) {
      result.push(`${nums[l]}->${nums[r]}`);
    } else {
      result.push(`${nums[l]}`);
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

**Оценка по времени:** O(n), где n - размер входного массива

**Оценка по памяти:** O(n), т.к. массив result в худшем случае будет состоять из n элементов

**Описание решения:**

Разбор темы: https://kinescope.io/wt5EkUf5jEi1eQRky8dseX
Разбор задачи: https://kinescope.io/13Qa7fgbQqA9NPyjihAVZP

1. В данном случае непересекающиеся окна. Ставим левый и правый указатели в начало массива.

2. Правый указатель двигается в случае, если следующий за ним элемент есть и он больше на 1.

3. Если условие для правого указателя не выполняется, то добавляем ответ в результирующий массив.

4. Двигаем оба указателя на `right + 1`.
