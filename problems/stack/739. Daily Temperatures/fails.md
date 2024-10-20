Лучше запоминать индекс каждого элемента в стеке и заносить значение в `result` в той последовательности, как и удаление из стека.

```typescript
function dailyTemperatures(temperatures: number[]): number[] {
  const result = new Array(temperatures.length).fill(0);
  const stack: number[] = [temperatures[0]];

  let pr = 0;
  let pt = 1;

  while (pt !== temperatures.length) {
    const t = temperatures[pt];

    if (stack.length !== 0 && t > stack.at(-1)) {
      result[pr] = pt - pr;
      stack.pop();
      pr++;
      continue;
    } else {
      stack.push(t);
      pt++;
    }
  }

  return result;
}
```
