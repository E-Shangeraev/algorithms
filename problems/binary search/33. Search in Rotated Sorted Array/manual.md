## Решение

```typescript
function findOffset(nums: number[], target: number): number {
  let l = -1;
  let r = nums.length - 1;

  while (r - l > 1) {
    const m = Math.floor((l + r) / 2);

    if (nums[m] > nums.at(-1)) {
      l = m;
    } else {
      r = m;
    }
  }

  return r;
}

function search(nums: number[], target: number): number {
  const offset = findOffset(nums, target);
  let l = offset;
  let r = nums.length + offset;

  while (r - l > 1) {
    const m = Math.floor((l + r) / 2);

    if (nums[m % nums.length] <= target) {
      l = m;
    } else {
      r = m;
    }
  }

  const index = l % nums.length;
  return nums[index] === target ? index : -1;
}
```

## Эталонное решение

```javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
const findOffset = function (nums) {
  // time: O(log n)
  // mem:  O(1)
  // good   bad
  // [   |  1 2 3 4 5]
  //   l    r

  //  good        bad
  // [4 5 6 7  |  0 1 2]
  //        l     r
  const good = i => {
    return nums[i] > nums[nums.length - 1];
  };

  let l = -1,
    r = nums.length - 1;
  while (r - l > 1) {
    let m = Math.floor((l + r) / 2);
    if (good(m)) {
      l = m;
    } else {
      r = m;
    }
  }
  return r;
};

/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number}
 */
var search = function (nums, target) {
  // time: O(log n)
  // mem:  O(1)
  const good = i => {
    return nums[i] <= target;
  };

  // обычный бинарный поиск, но смещаем на offset дополнительно
  let offset = findOffset(nums);
  let l = offset,
    r = nums.length + offset;
  while (r - l > 1) {
    // Note: ошибка №1 это делать "m = (l + r + offset) // 2"
    let m = Math.floor((l + r) / 2);
    if (good(m % nums.length)) {
      l = m;
    } else {
      r = m;
    }
  }
  // Note: ошибка №2 это забыть сделать "(l + offset) % len(nums)"
  let realLeft = l % nums.length;
  return nums[realLeft] === target ? realLeft : -1;
};
```

**Оценка по времени:** O(log n)

**Оценка по памяти:** O(1)

**Описание решения:**

https://kinescope.io/6xzekBiNBcMN5P9CtfBSJh

1. Сначала находим pivot индекс (или `offset` –– кол-во элементов, на которое был сдвинут массив). Пишем функцию `findOffset`,
   функцией `good` будет условие `nums[i] > nums[nums.length - 1]`. Тогда результатом будет правый индекс.

2. В основной функции представим, что наш массив не смещен. Левый указатель встанет на `offset`, а правый на `nums.length + offset`.

3. Производим обычный бинарный поиск. На каждой итерации у нас `m` будет тоже смещен, поэтому чтобы проверить на равенство таргету,
   мы приводим `m` к настоящему индексу (несмещенному) `m % nums.length`

4. В конце получаем смещенный `l`, который приводим к настоящему по той же формуле и делаем проверку на равенство таргету
