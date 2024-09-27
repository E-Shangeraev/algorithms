## Решение

```typescript
function rotate(nums: number[], k: number): void {
  k = k % nums.length;

  reverse(nums, 0, nums.length);
  reverse(nums, 0, k);
  reverse(nums, k, nums.length);
}

function reverse(nums: number[], from, to) {
  let left = from;
  let right = to - 1;

  while (left < right) {
    [nums[right], nums[left]] = [nums[left], nums[right]];

    left++;
    right--;
  }
}
```

**Оценка по времени:** O(n), где n - размер списка nums

**Оценка по памяти:** O(1), т.к. меняем исходный массив

**Описание решения:**

https://kinescope.io/2aH6yxJVfLXEHCaNVdFvCE

Решение через реверс подмассивов.

1. `k` может прийти больше размера исходного массива, поэтому преобразуем ее так, чтобы она всегда не первышала размер: `k = k % nums.length`

2. Можно воспользоваться встроенным методом `.reverse()` у массивов, но лучше написать свое решение. Реверс реализуется методом двух указателей с двух сторон.

3. Ревертим исходный массив

4. Ревертим подмассив от `0` до `k`

5. Ревертим подмассив от `k` до `nums.length`
