## Решение

```typescript
function subarraySum(nums: number[], k: number): number {
  const hashmap = new Map<number, number>([[0, 1]]);
  let sum = 0;
  let count = 0;

  for (const n of nums) {
    sum += n;

    const prefixSum = sum - k;

    if (hashmap.has(prefixSum)) {
      const prefixSumCount = hashmap.get(prefixSum);
      count += prefixSumCount;
    }

    const sumCount = hashmap.get(sum) ?? 0;
    hashmap.set(sum, sumCount + 1);
  }

  return count;
}
```

## Эталонное решение

```typescript
const subarraySum = (nums, targetSum) => {
  // ключ - префиксная сумма, значение - сколько раз встретили
  const prefixSums = { 0: 1 };

  // текущая префиксная сумма
  let currentPrefixSum = 0;

  // ответ
  let count = 0;
  for (const el of nums) {
    currentPrefixSum += el;

    // проверяем встречали ли мы уже префиксный массив с суммой currentPrefixSum - targetSum
    if (currentPrefixSum - targetSum in prefixSums) {
      // если встречали, то к ответу прибавлем число сколько раз уже встретили
      count += prefixSums[currentPrefixSum - targetSum];
    }

    // добавляем текущую префиксную сумму в мапу
    if (!(currentPrefixSum in prefixSums)) {
      prefixSums[currentPrefixSum] = 0;
    }
    prefixSums[currentPrefixSum]++;
  }
  return count;
};
```

**Оценка по времени:** O(n), где n - размер списка nums

**Оценка по памяти:** O(n), где n - размер списка nums, т.к. в худшем случае у нас создается мапа размера nums

**Описание решения:**

https://kinescope.io/jdxLNhW7RMyQRPRGPwpqCc

1. Создаем хешмапу для подсчета префиксных сумм: ключ - префиксная сумма, значение - сколько раз встретили

2. Проходимся по списку и на каждой итерации увеличиваем текущую префиксную сумму на текущее значение

3. На каждой итерации проверяем встречали ли мы уже префиксный массив с суммой currentPrefixSum - targetSum. Если встречали, то к ответу прибавлем число сколько раз уже встретили.

4. Добавляем текущую префиксную сумму в мапу
