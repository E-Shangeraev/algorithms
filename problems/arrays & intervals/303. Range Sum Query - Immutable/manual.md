## Решение

```typescript
class NumArray {
  nums: number[];
  px: number[];

  constructor(nums: number[]) {
    this.nums = nums;
    this.px = [0];
    this.fillPrefixArray();
  }

  fillPrefixArray(): void {
    this.nums.reduce((acc, cur) => {
      const sum = acc + cur;

      this.px.push(sum);

      return sum;
    }, 0);
  }

  sumRange(left: number, right: number): number {
    return this.px[right + 1] - this.px[left];
  }
}
```

**Оценка по времени:** O(n), где n - размер списка nums

**Оценка по памяти:** O(n), где n - размер списка nums

**Описание решения:**

Решение через префиксный массив

1. Заводим переменную для префиксного массива `px`, которой присваиваем массив с первым элементом 0

2. Заводим метод для заполнения префиксного массива (можно и без доп метода заполнять массив в конструкторе)

3. В качестве результата возвращаем разность элементов префиксного массива по индексам `right + 1` (т.к. получившийся префиксный массив на один элемент больше исходного) и `left` соответственно.
