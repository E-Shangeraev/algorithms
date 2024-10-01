## Решение

```typescript
function sortedSquares(nums: number[]): number[] {
  const result: number[] = new Array(nums.length);
  let left = 0;
  let right = nums.length - 1;
  let index = right;

  while (left <= right) {
    const lp = Math.pow(nums[left], 2);
    const rp = Math.pow(nums[right], 2);

    if (lp >= rp) {
      result[index] = lp;
      left++;
    } else {
      result[index] = rp;
      right--;
    }

    index--;
  }

  return result;
}
```

## Эталонное решение

```javascript
/**
 * @param {number[]} nums
 * @return {number[]}
 */
const sortedSquares = function (nums) {
  // храним массив квадратов в убывающем порядке
  let result = [];
  let p1 = 0; // указывает на начало массива
  let p2 = nums.length - 1; // указывает на конец массива
  while (p1 <= p2) {
    // больший элемент добавляем в конец ответа и двигаем указатель
    if (Math.abs(nums[p1]) > Math.abs(nums[p2])) {
      result.push(nums[p1] * nums[p1]);
      p1 += 1;
    } else {
      result.push(nums[p2] * nums[p2]);
      p2 -= 1;
    }
  }
  // разворачиваем список, чтобы получить возрастающий порядок
  return result.reverse();
};
```

https://kinescope.io/cG6U1BdXo1MoKxjvvksrHo

**Оценка по времени:** O(n), где n - размер массива nums

**Оценка по памяти:** O(n), где n - размер доп массива result

**Описание решения:**

1. Аллоцируем память под результирующий массив

2. Ставим указатель в начало и в конец массива

3. В цикле на каждой итерации сравниваем квадрат левого и правого числа. Какое число больше, то и добавляем в result

4. Есть 2 способа решения: добавлять все числа в конец массива и затем разворачивать его, либо хранить нужный индекс и по добавлять элемент по индексу. В любом случае это не влияет на ассимптотическую сложность
