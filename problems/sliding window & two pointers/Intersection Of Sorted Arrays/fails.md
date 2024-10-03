Неверно выбрал условие выхода из цикла

```javascript
module.exports = {
  //param A : array of integers
  //param B : array of integers
  //return a array of integers
  intersect: function (A, B) {
    const result = [];
    let p1 = 0;
    let p2 = 0;
    let n = Math.min(A.length, B.length);

    while (n >= 0) {
      if (A[p1] === B[p2]) {
        result.push(A[p1]);
        p1++;
        p2++;
        n--;
      }

      if (A[p1] > B[p2]) {
        p1++;
      } else {
        p2++;
      }
    }

    return result;
  },
};
```

Неверное условия. Возникают логические пересечения: `>=`, `<=` в рамках одной итерации

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
      }

      if (A[p1] > B[p2]) {
        p2++;
      } else {
        p1++;
      }
    }

    return result;
  },
};
```
