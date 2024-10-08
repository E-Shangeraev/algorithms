## Решение

```typescript
function search(nums: number[], target: number): number {
  let l = 0;
  let r = nums.length;

  const good = (i: number): boolean => nums[i] <= target;

  while (r - l > 1) {
    const mid = Math.floor((l + r) / 2);

    if (good(mid)) {
      l = mid;
    } else {
      r = mid;
    }
  }

  return nums[l] === target ? l : -1;
}
```

## Эталонное решение

```javascript
/**
 * @param {number} val
 * @param {number} target
 * @return {boolean}
 */
const good = (val, target) => {
  return val <= target;
};

/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function (nums, target) {
  // time: O(log n)
  // mem:  O(1)
  // ответ будет находится в элементе указывающим на l
  // поэтому сдвигаем r на 1 вправо, чтобы l мог принимать
  // значения [0, len(nums) - 1] т е от первого и до последнего
  // индекса включительно
  let l = 0,
    r = nums.length;
  while (r - l > 1) {
    let m = Math.floor((l + r) / 2);
    if (good(nums[m], target)) {
      l = m;
    } else {
      r = m;
    }
  }
  return nums[l] === target ? l : -1;
};
```

**Оценка по времени:** O(log n)

**Оценка по памяти:** O(1)

**Описание решения:**

Лекция по бинарному поиску: https://kinescope.io/h2B9dLETeinWuYeeNTDX9m
Разбор решения: https://leetcode.com/problems/binary-search/

1. Определяем что вернем в конце. В конце будем возвращать левый указатель, поэтому его ставим на 0, а правый указатель на `nums.length` (последний индекс + 1).

2. Пока разница между указателями не станет `1`, выполняем цикл.

3. На каждой итерации цикла находим средний элемент по формуле `Math.floor((l + r) / 2)`.

4. Определяем функцию `good`.

5. При выходе из цикла не забываем проверять, что под левым указателем стоит искомое число. Если это так, то возвращаем левый указатель, иначе `-1`.
