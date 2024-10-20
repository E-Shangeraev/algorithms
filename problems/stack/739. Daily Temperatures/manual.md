## Решение

```typescript
function dailyTemperatures(temperatures: number[]): number[] {
  const result = new Array(temperatures.length).fill(0);
  const stack: Record<string, number>[] = [{ value: temperatures[0], index: 0 }];

  let pt = 1;

  while (pt !== temperatures.length) {
    const t = temperatures[pt];
    const last = stack.at(-1);

    if (stack.length !== 0 && t > last.value) {
      result[last.index] = pt - last.index;
      stack.pop();
      continue;
    } else {
      stack.push({ value: t, index: pt });
      pt++;
    }
  }

  return result;
}
```

## Эталонное решение

```javascript
/**
 * @param {number[]} temperatures
 * @return {number[]}
 */
var dailyTemperatures = function (temperatures) {
  const result = new Array(temperatures.length).fill(0);
  // в стеке всегда храним убывающую последовательность
  // например: [[1, 20], [3, 8], [5, 1]]
  // [1, 20] -> в 1 день температура была 20
  const stack = [];
  for (let i = 0; i < temperatures.length; i++) {
    // пока текущая температура больше чем температура в стеке
    // вынимаем удаляем из стека элементы и
    // вычисляем для них ответ
    while (stack.length > 0 && stack[stack.length - 1][1] < temperatures[i]) {
      const [idx, _] = stack.pop();
      result[idx] = i - idx;
    }
    stack.push([i, temperatures[i]]);
  }
  return result;
};
```

**Оценка по времени:** O(n)

**Оценка по памяти:** O(n)

**Описание решения:**

https://kinescope.io/tefa1pMBeVmrKDPAPCPYAf

1. Аллоцируем память под результирующий массив, наполняем его нулями

2. Стек будет хранить убывающую последовательность температур

3. Как только встречаем значение больше, чем последнее в стеке, заносим по соответствующему индексу разницу между текущим и индексом и индексом элемента из стека

4. Если значение меньше последнего в стеке, заносим его в стек.
