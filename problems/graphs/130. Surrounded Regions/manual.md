## Решение

```typescript
/**
 Do not return anything, modify board in-place instead.
 */
function solve(board: string[][]): void {
  const visited = Array.from({ length: board.length }, () => Array(board[0].length).fill(false));

  // крайние столбы
  for (let i = 0; i < board.length; i++) {
    dfs(i, 0, visited, board, false);
    dfs(i, board[0].length - 1, visited, board, false);
  }

  // крайние строки
  for (let j = 0; j < board[0].length; j++) {
    dfs(0, j, visited, board, false);
    dfs(board.length - 1, j, visited, board, false);
  }

  for (let i = 0; i < board.length - 1; i++) {
    for (let j = 0; j < board[i].length - 1; j++) {
      dfs(i, j, visited, board, true);
    }
  }
}

function dfs(i: number, j: number, visited: boolean[][], board: string[][], flip: boolean): void {
  if (i < 0 || i >= board.length || j < 0 || j >= board[0].length) return;

  if (visited[i][j] || board[i][j] === 'X') return;

  visited[i][j] = true;

  if (flip) {
    board[i][j] = 'X';
  }

  const steps = [
    [0, -1],
    [-1, 0],
    [0, 1],
    [1, 0],
  ];

  for (const step of steps) {
    const nextI = i + step[0];
    const nextJ = j + step[1];

    dfs(nextI, nextJ, visited, board, flip);
  }
}
```

## Эталонное решение

```javascript
/**
 * @param {character[][]} board
 * @return {void} Do not return anything, modify board in-place instead.
 */
var solve = function (board) {
  const visited = Array(board.length)
    .fill(null)
    .map(() => Array(board[0].length).fill(false));

  // перебираем крайние строки
  for (let i = 0; i < board.length; i++) {
    dfs(i, 0, visited, board, false);
    dfs(i, board[0].length - 1, visited, board, false);
  }

  // перебираем крайние столбцы
  for (let i = 0; i < board[0].length; i++) {
    dfs(0, i, visited, board, false);
    dfs(board.length - 1, i, visited, board, false);
  }

  // обходим все индексы кроме крайних - т к их уже обходили
  for (let i = 1; i < board.length - 1; i++) {
    for (let j = 1; j < board[i].length - 1; j++) {
      // bfs запускаем только для не посещенных вершин - проверка внутри
      dfs(i, j, visited, board, true);
    }
  }
};

const dfs = (startX, startY, visited, board, flip) => {
  if (!goodIdx(startX, startY, board)) {
    return;
  }
  // dfs запускаем только для не посещенных вершин
  if (visited[startX][startY] || board[startX][startY] === 'X') {
    return;
  }

  visited[startX][startY] = true;
  if (flip) {
    board[startX][startY] = 'X';
  }

  const steps = [
    [0, 1],
    [0, -1],
    [1, 0],
    [-1, 0],
  ];
  // перебераем шаги которые могут быть из текущий вершины
  for (const step of steps) {
    // вычисляем координаты куда можем пойти
    const newX = startX + step[0];
    const newY = startY + step[1];
    dfs(newX, newY, visited, board, flip);
  }
};

const goodIdx = (i, j, board) => {
  return 0 <= i && i < board.length && 0 <= j && j < board[0].length;
};
```

**Оценка по времени:** O(n \* m)

**Оценка по памяти:** O(n \* m)

**Описание решения:**

https://www.youtube.com/watch?v=gPZ-LGDxyT4

Можно решать, как через DFC, так и через BFS. В данном случае решение представлено через DFS.

1. Заводим матрицу `visited`, которая будет хранить клетки, которые уже обошли.

2. Обходим сперва границы и помечаем клетки, как посещенные. Важно: во время обхода границ не меняем значения клеток в `board`.

3. Обходим каждый элемент и запускаем рекурсивную функцию dfs.

4. Функция dfs кладет переданную в нее клетку в матрицу `visited` и проверяет клетки по вертикали и горизонтали вокруг нее.
