const board = Array(9).fill(null);
const human = 'O';
const ai = 'X';

document.querySelectorAll('.cell').forEach(cell => cell.addEventListener('click', onCellClick));

function onCellClick(e) {
    const index = e.target.getAttribute('data-index');
    if (board[index] || checkWinner()) return;

    board[index] = human;
    e.target.textContent = human;

    if (!checkWinner() && board.includes(null)) {
        const bestMove = minimax(board, ai).index;
        board[bestMove] = ai;
        document.querySelector(`.cell[data-index='${bestMove}']`).textContent = ai;
    }
    
    if (checkWinner()) {
        alert(checkWinner() === 'tie' ? "It's a Tie!" : `${checkWinner()} Wins!`);
    }
}

function checkWinner() {
    const winConditions = [
        [0, 1, 2], [3, 4, 5], [6, 7, 8],
        [0, 3, 6], [1, 4, 7], [2, 5, 8],
        [0, 4, 8], [2, 4, 6]
    ];

    for (const condition of winConditions) {
        const [a, b, c] = condition;
        if (board[a] && board[a] === board[b] && board[a] === board[c]) {
            return board[a];
        }
    }

    if (!board.includes(null)) return 'tie';
    return null;
}

function minimax(newBoard, player) {
    const emptyIndexes = newBoard.reduce((acc, el, i) => el === null ? acc.concat(i) : acc, []);

    if (checkWinner() === human) return { score: -10 };
    if (checkWinner() === ai) return { score: 10 };
    if (emptyIndexes.length === 0) return { score: 0 };

    const moves = [];
    for (const i of emptyIndexes) {
        const move = { index: i };
        newBoard[i] = player;

        if (player === ai) {
            move.score = minimax(newBoard, human).score;
        } else {
            move.score = minimax(newBoard, ai).score;
        }

        newBoard[i] = null;
        moves.push(move);
    }

    return player === ai
        ? moves.reduce((best, move) => move.score > best.score ? move : best)
        : moves.reduce((best, move) => move.score < best.score ? move : best);
}

function resetGame() {
    board.fill(null);
    document.querySelectorAll('.cell').forEach(cell => cell.textContent = '');
}
