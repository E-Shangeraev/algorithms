## Решение

```typescript
function backspaceCompare(s: string, t: string): boolean {
  let p1 = 0;
  let p2 = 0;

  while (p1 < s.length) {
    if (s[p1] === '#') {
      if (p1 !== 0) {
        s = s.slice(0, p1 - 1) + s.slice(p1 + 1);
        p1--;
      } else {
        s = s.slice(1);
      }
      continue;
    }

    p1++;
  }

  while (p2 < t.length) {
    if (t[p2] === '#') {
      if (p2 !== 0) {
        t = t.slice(0, p2 - 1) + t.slice(p2 + 1);
        p2--;
      } else {
        t = t.slice(1);
      }
      continue;
    }

    p2++;
  }

  return s === t;
}
```

## Эталонное решение

```javascript
/**
 * @param {string} s
 * @param {number} i
 * @return {number}
 */
const findNextNonSkip = function (s, i) {
  let skipCount = 0;
  while (i >= 0 && (skipCount > 0 || s[i] === '#')) {
    if (s[i] === '#') {
      skipCount += 1;
      i -= 1;
      continue;
    }
    skipCount -= 1;
    i -= 1;
  }
  return i;
};

/**
 * @param {string} s
 * @param {string} t
 * @return {boolean}
 */
const backspaceCompare = function (s, t) {
  let p1 = s.length;
  let p2 = t.length;
  while (p1 > 0 && p2 > 0) {
    p1 = findNextNonSkip(s, p1 - 1);
    p2 = findNextNonSkip(t, p2 - 1);
    if (p1 >= 0 && p2 >= 0 && s[p1] !== t[p2]) {
      return false;
    }
  }
  return findNextNonSkip(s, p1 - 1) === findNextNonSkip(t, p2 - 1);
};
```

**Оценка по времени:** O(n + m), где n и m - длины строк s и t соответственно

**Оценка по памяти:** O(1), т.к. не выделяем доп память

**Описание решения:**

https://kinescope.io/3kccYN5ohjsnBe4gUJdZJQ

Описываться будет эталонное решение, т.к. собственное не такое эффективное

1. Ставим по указателю в конец каждой строки

2. Если встречаем `#`, то начинаем вести счетчик: решетка увеличивает счетчик на 1, буква уменьшает на 1

3. Если указатели еще не вышли за пределы строк, но указывают на разные буквы - возвращаем `false`

4. В конце сравниваем индексы двух указателей.
