## Решение

```typescript
function missingNumber(nums: number[]): number {
  const hashset = new Set<number>();
  const n = nums.length;

  for (const num of nums) {
    hashset.add(num);
  }

  for (const num of nums) {
    if (!hashset.has(n - num)) {
      return n - num;
    }
  }

  return 1;
}
```

**Оценка по времени:** O(n), где n - размер списка nums

**Оценка по памяти:** O(n), где n - размер списка nums, т.к. в худшем случае у нас создается мапа размера nums

## Эталонное решение

```typescript
const missingNumber = nums => {
  let overallSum = 0;
  for (let i = 0; i <= nums.length; i++) {
    overallSum += i;
  }
  for (const num of nums) {
    overallSum -= num;
  }
  return overallSum;
};
```

**Оценка по времени:** O(n), где n - размер списка nums

**Оценка по памяти:** O(1), т.к. не используем доп память

**Описание решения:**

https://kinescope.io/6L4Nq8hPz6vz2XbuzpKU7r

1. Все элементы по условию могут быть только от 0 до n, где n - длина массива. Пропущено одно единственное число. Считаем сумму всех чисел в диапазоне [0, n].

2. Далее из всей получившейся суммы необходимо вычесть сумму элементов исходного массива. Полученное число и будет нашим результатом.
