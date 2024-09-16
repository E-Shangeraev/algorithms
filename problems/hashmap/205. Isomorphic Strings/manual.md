## Решение

```typescript
function isIsomorphic(s: string, t: string): boolean {
  if (s.length !== t.length) return false;

  const hashmap1 = new Map<string, string>();
  const hashmap2 = new Map<string, string>();

  for (let i = 0; i < s.length; i++) {
    const sChar = s.charAt(i);
    const tChar = t.charAt(i);

    if (!hashmap1.has(sChar)) {
      hashmap1.set(sChar, tChar);
    }

    if (!hashmap2.has(tChar)) {
      hashmap2.set(tChar, sChar);
    }

    if (hashmap1.get(sChar) !== tChar || hashmap2.get(tChar) !== sChar) {
      return false;
    }
  }

  return true;
}
```

**Оценка по времени:** O(n), где n - длина любой строки (если строки разной длины, то они не изоморфны)

**Оценка по памяти:** O(n), где n - длина любой строки

**Описание решения:** Используем 2 хешмапы, где у каждой ключ соответствуют символу строки, а значение символу другой строки. Если строки разной длины - сразу возвращаем false. Важно не перезаписывать уже имеющиеся значения в мапе, потому что в таком случае у нас всегда будет true.
