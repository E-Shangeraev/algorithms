## Решение

```typescript
function isMonotonic(nums: number[]): boolean {
  if (nums.length <= 2) return true;

  let isIncreasing = true;
  let isDecreasing = true;

  for (let i = 1; i < nums.length; i++) {
    isIncreasing = isIncreasing && nums[i] >= nums[i - 1];
    isDecreasing = isDecreasing && nums[i] <= nums[i - 1];
  }

  return isIncreasing || isDecreasing;
}
```

**Оценка по времени:** O(n), где n - размер списка nums

**Оценка по памяти:** O(1), т.к. заводим всего две переменные типа boolean

**Описание решения:**

1. Заводим 2 флага: isIncreasing и isDecreasing. Заранее выставляем их в true

2. Каждый флаг может установиться в false только 1 раз, поэтому мы меняем флаг только, если он до этого был true

3. В качестве результата нас интересует либо монотонное возрастание, либо монотонное убывание массива
