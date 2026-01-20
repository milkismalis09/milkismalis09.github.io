# milkismalis09.github.io
Chess
<!DOCTYPE html><html lang="ru">
<head>
  <meta charset="UTF-8" />
  <title>Шахматы</title>
  <style>
    body {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
      background: #1e1e1e;
      font-family: Arial, sans-serif;
    }
    .board {
      display: grid;
      grid-template-columns: repeat(8, 70px);
      grid-template-rows: repeat(8, 70px);
      border: 4px solid #333;
    }
    .cell {
      width: 70px;
      height: 70px;
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 40px;
      cursor: pointer;
      user-select: none;
    }
    .white { background: #f0d9b5; }
    .black { background: #b58863; }
    .selected { outline: 4px solid red; }
  </style>
</head>
<body><div class="board" id="board"></div><script>
  const boardElement = document.getElementById('board');

  const pieces = {
    r: '♜', n: '♞', b: '♝', q: '♛', k: '♚', p: '♟',
    R: '♖', N: '♘', B: '♗', Q: '♕', K: '♔', P: '♙'
  };

  let board = [
    'rnbqkbnr',
    'pppppppp',
    '........',
    '........',
    '........',
    '........',
    'PPPPPPPP',
    'RNBQKBNR'
  ];

  let selected = null;

  function drawBoard() {
    boardElement.innerHTML = '';
    for (let y = 0; y < 8; y++) {
      for (let x = 0; x < 8; x++) {
        const cell = document.createElement('div');
        cell.className = 'cell ' + ((x + y) % 2 === 0 ? 'white' : 'black');
        const piece = board[y][x];
        if (piece !== '.') cell.textContent = pieces[piece];
        cell.onclick = () => onCellClick(x, y, cell);
        boardElement.appendChild(cell);
      }
    }
  }

  function onCellClick(x, y, cell) {
    if (selected) {
      movePiece(selected.x, selected.y, x, y);
      selected = null;
      drawBoard();
    } else if (board[y][x] !== '.') {
      selected = { x, y };
      cell.classList.add('selected');
    }
  }

  function movePiece(x1, y1, x2, y2) {
    let b = board.map(row => row.split(''));
    b[y2][x2] = b[y1][x1];
    b[y1][x1] = '.';
    board = b.map(row => row.join(''));
  }

  drawBoard();
</script></body>
</html>
