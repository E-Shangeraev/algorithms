https://www.interviewbit.com/problems/balanced-parantheses/

## Решение

```javascript
module.exports = {
  //param A : string
  //return an integer
  solve: function (A) {
    let balance = 0;

    for (const char of A) {
      if (char === '(') {
        balance++;
      } else if (char === ')' && balance !== 0) {
        balance--;
      } else {
        return 0;
      }
    }

    return balance === 0 ? 1 : 0;
  },
};
```

**Оценка по времени:** O(n)

**Оценка по памяти:** O(1)

**Описание решения:**

1. Определяем переменную balance, которая на открывающиеся скобки будет увеличиваться на 1, а при закрывающейся уменьшаться на 1.

2. Следует помнить, что последовательность может начинаться с закрывающихся скобок `))(()())`. Поэтому следует дополнительно для закрывающихся скобок делать проверку `balance !== 0`. В противном случае строка невалидна –– можно сразу возвращать 0.
