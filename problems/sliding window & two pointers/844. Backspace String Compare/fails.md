Не учел, что решетка может стоять в начале строки

```typescript
function backspaceCompare(s: string, t: string): boolean {
  let p1 = 0;
  let p2 = 0;

  while (p1 < s.length) {
    if (s[p1] === '#') {
      s = s.slice(0, p1 - 1) + s.slice(p1 + 1);
      p1--;
      continue;
    }

    p1++;
  }

  while (p2 < t.length) {
    if (t[p2] === '#') {
      t = t.slice(0, p2 - 1) + t.slice(p2 + 1);
      p2--;
      continue;
    }

    p2++;
  }

  return s === t;
}
```
