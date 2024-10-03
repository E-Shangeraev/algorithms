## Решение

```javascript
module.exports = {
  //param A : array of integers
  //param B : array of integers
  //return a array of integers
  intersect: function (A, B) {
    const result = [];
    let p1 = 0;
    let p2 = 0;

    while (p1 < A.length && p2 < B.length) {
      if (A[p1] === B[p2]) {
        result.push(A[p1]);
        p1++;
        p2++;
      } else if (A[p1] > B[p2]) {
        p2++;
      } else {
        p1++;
      }
    }

    return result;
  },
};
```

## Эталонное решение

```javascript
module.exports = {
  //param A : array of integers
  //param B : array of integers
  //return a array of integers
  intersect: function (A, B) {
    let p1 = 0;
    let p2 = 0;
    let res = [];
    // т к мы можем иметь дубликаты то на каждой итерации сравниваем на
    // равестно и если равны двигаем оба указателя и прибавляем ответ
    // иначе двигаем указатель который указывает на меньшее значение
    while (p1 < A.length && p2 < B.length) {
      if (A[p1] > B[p2]) {
        p2 += 1;
      } else if (A[p1] < B[p2]) {
        p1 += 1;
      } else {
        res.push(A[p1]);
        p1 += 1;
        p2 += 1;
      }
    }
    return res;
  },
};
```

**Оценка по времени:** O(n + m), где n - размер A, m - размер B

**Оценка по памяти:** O(min(n, m)), т.к. в худшем случае у нас пересекутся все элементы из меньшего массива

**Описание решения:**

https://kinescope.io/sKeBVfQQTfrdxkS1VPYrdd

Каждому по указателю. Т.к. мы можем иметь дубликаты то на каждой итерации сравниваем на равестно и если равны двигаем оба указателя и прибавляем ответ в `result`, иначе двигаем указатель который указывает на меньшее значение
