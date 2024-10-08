## Решение

```typescript
function searchFirstTarget(nums: number[], target: number): number {
  let l = -1;
  let r = nums.length - 1;

  while (r - l > 1) {
    const m = Math.floor((l + r) / 2);

    if (nums[m] < target) {
      l = m;
    } else {
      r = m;
    }
  }

  return nums[r] === target ? r : -1;
}

function searchLastTarget(nums: number[], target: number): number {
  let l = 0;
  let r = nums.length;

  while (r - l > 1) {
    const m = Math.floor((l + r) / 2);

    if (nums[m] <= target) {
      l = m;
    } else {
      r = m;
    }
  }

  return nums[l] === target ? l : -1;
}

function searchRange(nums: number[], target: number): number[] {
  if (nums.length === 0) return [-1, -1];

  let first = searchFirstTarget(nums, target);
  let last = searchLastTarget(nums, target);

  return [first, last];
}
```

## Эталонное решение

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchLastTarget = function (nums, target) {
  // ответ будет находится в элементе указывающим на l
  // поэтому сдвигаем r на 1 вправо, чтобы l мог принимать
  // значения [0, len(nums) - 1] т е от первого и до последнего
  // индекса включительно
  let l = 0;
  let r = nums.length;
  while (r - l > 1) {
    let m = Math.floor((l + r) / 2);
    if (nums[m] <= target) {
      l = m;
    } else {
      r = m;
    }
  }
  return nums[l] === target ? l : -1;
};

/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var searchFirstTarget = function (nums, target) {
  // ответ будет находится в элементе указывающим на r
  // поэтому сдвигаем l на 1 влево, чтобы r мог принимать
  // значения [0, len(nums) - 1] т е от первого и до последнего
  // индекса включительно
  let l = -1;
  let r = nums.length - 1;
  while (r - l > 1) {
    let m = Math.floor((l + r) / 2);
    if (nums[m] < target) {
      l = m;
    } else {
      r = m;
    }
  }
  return nums[r] === target ? r : -1;
};

/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
var searchRange = function (nums, target) {
  if (nums.length === 0) {
    return [-1, -1];
  }
  let l = searchFirstTarget(nums, target);
  let r = searchLastTarget(nums, target);
  return [l, r];
};
```

**Оценка по времени:** O(log n)

**Оценка по памяти:** O(1)

**Описание решения:**

https://kinescope.io/vCa43hvTVnhXXFL3VS3FM5

1. Тут нужно 2 раза выполнить бинарный поиск: для поиска первого и второго вхождений. В зависимости от этого будут разные левые и правые указатели. Проще всего определиться с указателями и условиями будет на примере одинаковых элементов массива, например: `[3, 3, 3]`.

2. На первое вхождение будет указывать правый указатель и условием "хороших" элементов будет `nums[m] < target`.

3. На последнее вхождение будет указывать левый указатель и условием "хороших" элементов будет `nums[m] <= target`.
