## Решение

```typescript
function findMaxConsecutiveOnes(nums: number[]): number {
  let left = 0;
  let right = 0;
  let result = 0;

  while (left < nums.length) {
    while (right < nums.length && nums[right] !== 0) {
      right++;
    }

    result = Math.max(result, right - left);

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
 * @return {number}
 */
const findMaxConsecutiveOnes = function (nums) {
  let l = 0;
  let r = 0;
  let result = 0;
  while (l < nums.length) {
    // before
    // l
    // 1 1 1 1 0 0 1 1
    // r

    // бежим правым указателем пока в интервале [l, r]
    // находятся все последовательные числа
    while (r + 1 < nums.length && nums[r] === nums[r + 1]) {
      r += 1;
    }
    // after
    // l
    // 1 1 1 1 0 0 1 1
    //       r

    // обновляем ответ только если в палавающем окне были 1-цы
    // нас не просят искать нули, поэтому окна с нулями игнорируем
    if (nums[r] === 1) {
      result = Math.max(result, r - l + 1);
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

**Оценка по времени:** O(n), где n - длина массива nums

**Оценка по памяти:** O(1), т.к. создаем только числовые переменные

**Описание решения:**

Разбор темы: https://kinescope.io/wt5EkUf5jEi1eQRky8dseX
Разбор задачи: https://kinescope.io/dWAqbVXTbKJpHuBdmPMmn8

1. В данном случае непересекающиеся окна. Ставим левый и правый указатели в начало массива.

2. Правый указатель двигается до тех пор пока не встрети 0.

3. Если условие для правого указателя не выполняется, то выходим из цикла обновляем максимальное значение последовательности. Текущая последовательность считается как разность правого и левого указателей.

4. Двигаем оба указателя на `right + 1`.
