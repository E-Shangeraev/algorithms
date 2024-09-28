## Решение

```typescript
function minimumDifference(nums: number[], k: number): number {
  let min = Infinity;
  let left = 0;
  let right = k - 1;

  nums.sort((a, b) => a - b);

  while (right < nums.length) {
    const diff = nums[right] - nums[left];

    min = Math.min(min, diff);

    left++;
    right++;
  }

  return min;
}
```

## Эталонное решение

```javascript
const minimumDifference = (nums, k) => {
  let result = Infinity;

  nums.sort((a, b) => a - b);

  let p1 = 0;
  let p2 = k - 1;

  while (p2 < nums.length) {
    result = Math.min(result, nums[p2] - nums[p1]);
    p1++;
    p2++;
  }
  return result;
};
```

**Оценка по времени:** O(n\*logn), где n - размер списка nums, а метод `sort` использует быструю сортировку

**Оценка по памяти:** O(1), т.к. не выделяем доп память

**Описание решения:**

1. Сортируем массив. Это позволяет расположить элементы с минимальной разницей рядом друг с другом

2. Ставим левый указатель на `0` индекс и правый на `k - 1` индекс

3. Итерируемся по списку и ищем минимальную разницу
