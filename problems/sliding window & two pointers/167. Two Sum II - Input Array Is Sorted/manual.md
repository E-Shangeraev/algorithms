## Решение

```typescript
function twoSum(numbers: number[], target: number): number[] {
  let left = 0;
  let right = numbers.length - 1;

  while (left < right) {
    const sum = numbers[left] + numbers[right];

    if (sum === target) {
      return [left + 1, right + 1];
    }

    if (sum > target) {
      right--;
    }

    if (sum < target) {
      left++;
    }
  }

  return [];
}
```

## Эталонное решение

```javascript
/**
 * @param {number[]} nums
 * @param {number} target
 * @return {number[]}
 */
const twoSum = (nums, target) => {
  let l = 0;
  let r = nums.length - 1;

  while (l < r) {
    let currSum = nums[l] + nums[r];
    // если текущая сумма равна target
    // -> возвращаем индексы пары чисел
    if (currSum === target) {
      return [l + 1, r + 1];
    }
    // если текущая сумма больше target
    // -> сдвигаем правый указатель чтобы уменьшить общую сумму
    else if (currSum > target) {
      r -= 1;
    }
    // если текущая сумма больше target
    // -> сдвигаем левый указатель чтобы увеличить общую сумму
    else {
      l += 1;
    }
  }

  return [-1, -1];
};
```

**Оценка по времени:** O(n), где n - размер массива

**Оценка по памяти:** O(1), т.к. не выделяем доп память

**Описание решения:**

https://kinescope.io/c6yKmiiBWqYczvBVqsWDLx

1. Метод двух указателей с двух сторон. Ставим один указатель в начало списка и другой в конец.

2. Т.к. список отсортированный, то при превышении суммы двигаем правый указатель влево, а если полученная сумма меньше таргета, то двигаем левый указатель вправо

3. При равенстве полученной суммы и таргета возвращаем `[left + 1, right + 1]`
