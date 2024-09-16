## Решение

```typescript
function isValidSudoku(board: string[][]): boolean {
  const rows = new Set<string>();
  const cols = new Set<string>();
  const boxes = new Set<string>();

  for (let i = 0; i < board.length; i++) {
    for (let j = 0; j < board[i].length; j++) {
      const current = board[i][j];

      if (isNaN(+current)) {
        continue;
      }

      const rowElement = `[${i}, ${current}]`;

      if (rows.has(rowElement)) {
        return false;
      } else {
        rows.add(rowElement);
      }

      const colElement = `[${j}, ${current}]`;

      if (cols.has(colElement)) {
        return false;
      } else {
        cols.add(colElement);
      }

      const boxIndex = Math.floor(i / 3) * 3 + Math.floor(j / 3);
      const boxElement = `[${boxIndex}, ${current}]`;

      if (boxes.has(boxElement)) {
        return false;
      } else {
        boxes.add(boxElement);
      }
    }
  }

  return true;
}
```

**Оценка по времени:** O(1), т.к. у нас матрица заданной длины

**Оценка по памяти:** O(1), т.к. у нас матрица заданной длины

**Описание решения:** Используем 3 хешсета, где каждое значение - это строк, содержащая соответствующий индекс (в строке, колонке или боксе) и само значение. Каждый бокс тоже имеет индекс, который вычисляется по формуле:

`Math.floor(i / 3) * 3 + Math.floor(j / 3)`

Следует помнить, что в TypeScript функция isNaN не принимает ничего, кроме `number` и `NaN`.
