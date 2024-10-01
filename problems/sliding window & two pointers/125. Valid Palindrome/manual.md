## Решение

```typescript
function isPalindrome(s: string): boolean {
  let left = 0;
  let right = s.length - 1;

  while (left <= right) {
    if (!isLetter(s[left])) {
      left++;
      continue;
    }

    if (!isLetter(s[right])) {
      right--;
      continue;
    }

    if (s[left].toLowerCase() !== s[right].toLowerCase()) {
      return false;
    }

    left++;
    right--;
  }

  return true;
}

function isLetter(char: string): boolean {
  return char.toUpperCase() !== char.toLowerCase() || !isNaN(Number.parseFloat(char));
}
```

## Эталонное решение

```javascript
/**
 * @param {string} s
 * @return {boolean}
 */
const isPalindrome = s => {
  let l = 0;
  let r = s.length - 1;
  while (l < r) {
    if (!s[l].match(/[a-zA-Z0-9]/)) {
      l++;
      continue;
    }
    if (!s[r].match(/[a-zA-Z0-9]/)) {
      r--;
      continue;
    }
    if (s[l].toLowerCase() !== s[r].toLowerCase()) {
      return false;
    }
    l++;
    r--;
  }
  return true;
};
```

**Оценка по времени:** O(n), где n - длина строки

**Оценка по памяти:** O(1), т.к. не аллоцируется доп память

**Описание решения:**

https://kinescope.io/s9YYQkqxwKioSSPPXDNWrw

1. Решение методом двух указателей с двух сторон. Основная сложность отделить строчное значение от других символов. Для этого можно написать функцию хелпер, либо воспользоваться регуляркой

2. На каждой итерации сперва проверяем, что символ является буквой. Если не является, то сдвигаем соответствующий указатель и продолжаем цикл. Если является - сравниваем две буквы в нижнем регистре и если они не равны возвращаем `false`

3. Если цикл завершился успешно, то возвращаем `true`
