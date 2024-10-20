## Решение

```typescript
function minRemoveToMakeValid(s: string): string {
  let result: string[] = s.split('');
  const stack: number[] = [];

  for (let i = 0; i < s.length; i++) {
    const char = s[i];

    if (char === '(') {
      stack.push(i);
    } else if (char === ')' && stack.length === 0) {
      result[i] = '';
    } else if (char === ')' && stack.length !== 0) {
      stack.pop();
    }
  }

  for (const i of stack) {
    result[i] = '';
  }

  return result.join('');
}
```

## Эталонное решение

```javascript
/**
 * @param {string} s
 * @return {string}
 */
var minRemoveToMakeValid = function (s) {
  // в python строки не изменяемы поэтому нужно сделать список из символов
  // который уже можно менять
  const result = s.split('');
  const stack = []; // храним индексы для символа (
  for (let i = 0; i < result.length; i++) {
    const char = result[i];
    if (char === '(') {
      stack.push(i);
    } else if (char === ')' && stack.length === 0) {
      // скобка ")" лишняя и должна быть удалена
      result[i] = '';
    } else if (char === ')' && stack.length !== 0) {
      stack.pop();
    }
  }

  // проходимся по всем лишним скобкам "(" и удаляем их
  for (let i of stack) {
    result[i] = '';
  }

  // делаем строку из элементов списка
  return result.join('');
};
```

**Оценка по времени:** O(n)

**Оценка по памяти:** O(n)

**Описание решения:**

https://kinescope.io/4bMWrHYdM48YbMERFShsfe

1. Создаем стек для хранения лишних открывающихся скобок.

2. Если скобка закрывающаяся стек пустой, то скобка лишняя и ее удаляем. Если скобка закрывающаяся, а стек непустой, удаляем из стека последнюю открывающуюся скобку.

3. В конце проходимся по всем оставшимся лишних открывающимся скобками и удаляем их из ответа.
