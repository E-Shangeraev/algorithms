Ошибки по невнимательности: сравниваю не средний элемент в строке, а самый левый и переприсваиваю `m`, вместо `l` и `r`.

```typescript
function searchInRow(row: number[], target: number) {
  let l = 0;
  let r = row.length;

  while (r - l > 1) {
    let m = Math.floor((r + l) / 2);

    if (row[l] <= target) {
      m = l;
    } else {
      m = r;
    }
  }

  return row[l] === target ? l : -1;
}

function searchMatrix(matrix: number[][], target: number): boolean {
  let l = 0;
  let r = matrix.length;

  while (r - l > 1) {
    let m = Math.floor((r + l) / 2);
    const row = matrix[m];

    if (row[0] <= target) {
      l = m;
    } else {
      r = m;
    }
  }

  const index = searchInRow(matrix[l], target);

  return index !== -1;
}
```

================================================================

```typescript
function searchInRow(row: number[], target: number) {
  let l = 0;
  let r = row.length;

  while (r - l > 1) {
    let m = Math.floor((r + l) / 2);

    if (row[l] <= target) {
      l = m;
    } else {
      r = m;
    }
  }

  return row[l] === target ? l : -1;
}

function searchMatrix(matrix: number[][], target: number): boolean {
  let l = 0;
  let r = matrix.length;

  while (r - l > 1) {
    let m = Math.floor((r + l) / 2);
    const row = matrix[m];

    if (row[0] <= target) {
      l = m;
    } else {
      r = m;
    }
  }

  const index = searchInRow(matrix[l], target);

  return index !== -1;
}
```
