## Решение

```typescript
function searchInRow(row: number[], target: number) {
  let l = 0;
  let r = row.length;

  while (r - l > 1) {
    let m = Math.floor((r + l) / 2);

    if (row[m] <= target) {
      l = m;
    } else {
      r = m;
    }
  }

  return row[l] === target ? l : -1;
}

function searchMatrix(matrix: number[][], target: number): boolean {
  let l = 0;
  let r = matrix.length;

  while (r - l > 1) {
    let m = Math.floor((r + l) / 2);
    const row = matrix[m];

    if (row[0] <= target) {
      l = m;
    } else {
      r = m;
    }
  }

  const index = searchInRow(matrix[l], target);

  return index !== -1;
}
```

## Эталонное решение

```javascript
/**
 * @param {number[][]} matrix
 * @param {number} target
 * @return {boolean}
 */
var searchMatrix = function (matrix, target) {
  // time: O(log (N * M))
  // mem:  O(1)
  // чтобы работать с 2-D массивом как с 1-D
  const elementFromMatrix = i => {
    let n = matrix[0].length;
    return matrix[Math.floor(i / n)][i % n];
  };

  const good = i => {
    return elementFromMatrix(i) <= target;
  };

  // обычный бинарный поиск как для 1-D массива
  let l = 0,
    r = matrix.length * matrix[0].length;
  while (r - l > 1) {
    let m = Math.floor((l + r) / 2);
    if (good(m)) {
      l = m;
    } else {
      r = m;
    }
  }
  return elementFromMatrix(l) === target;
};
```

**Оценка по времени:** O(log(n \* m))

**Оценка по памяти:** O(1)

**Описание решения:**

https://kinescope.io/0GboubeRnaMB9Mmajrex4p

Будет описано эталонное решение.

1. У матрицы элементы идут строго по возрастанию, поэтому ее можно представить в виде одномерного массива. Левый указатель ставим на `0`, а правый на последний элемент в матрице `matrix.length * matrix[0].length`.

2. Мы преобразуем индекс в номер строки согласно формуле деления без остатка `Math.floor(i / n)`, а индекс колонки –– по формуле получения остатка от деления `i % n`.

3. Используем полученный элемент в функции `good`

4. В конце `l` указывает на результат. Не забываем получить элемент по индексу и сравнить с `target`.
