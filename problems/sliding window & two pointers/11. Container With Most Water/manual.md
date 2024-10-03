## Решение

```typescript
function maxArea(height: number[]): number {
  let left = 0;
  let right = height.length - 1;
  let maxAmount = 0;

  while (left <= right) {
    const width = right - left;
    const maxHeight = Math.min(height[left], height[right]);
    maxAmount = Math.max(maxAmount, width * maxHeight);

    if (height[left] < height[right]) {
      left++;
    } else {
      right--;
    }
  }

  return maxAmount;
}
```

## Эталонное решение

```javascript
/**
 * @param {number[]} height
 * @return {number}
 */
var maxArea = function (height) {
  let l = 0;
  let r = height.length - 1;
  let resultArea = 0;
  while (l < r) {
    // текущая площадь ограниченная l и r
    let currArea = Math.min(height[l], height[r]) * (r - l);
    // обновляем максимальную площадь
    resultArea = Math.max(resultArea, currArea);
    // Сдвигаем указатель, который указывает на меньшую высоту
    if (height[l] < height[r]) {
      l += 1;
    } else {
      r -= 1;
    }
  }
  return resultArea;
};
```

**Оценка по времени:** O(n), где n - размер списка height

**Оценка по памяти:** O(1), т.к. не выделяем доп память

**Описание решения:**

https://kinescope.io/coJf2KTHRUmBAdjH4zUb9J

1. Метод двух указателей с двух сторон. Находим ширину аквариума (разность указателей)

2. Находим текущую _максимально возможную_ высоту (которая является минимальной из двух высот)

3. Обновляем максимальную площадь

4. Если высота слева меньше высоты справа, то сдвигаем левый указатель вправо, иначе - правый указатель влево
