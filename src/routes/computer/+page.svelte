<script>
    let squares = $state(Array(9).fill(null));
    let playerX = $state(true);
    let playerXMoves = $state([]);
    let playerOMoves = $state([]);
    let xCounter = $state(0);
    let oCounter = $state(0);

    const handleClick = (index) => {
        if (squares[index] || calculateWinner(squares)) return;

        if (playerX) {
            xCounter += 1;
        } else {
            oCounter += 1;
        }

        if (xCounter === 4) {
            xCounter -= 1;
            const move = playerXMoves.shift();
            squares[move] = null;
        } else if (oCounter === 4) {
            oCounter -= 1;
            const move = playerOMoves.shift();
            squares[move] = null;
        }

        squares[index] = playerX ? "X" : "O";

        if (playerX) {
            playerXMoves.push(index);
        } else {
            playerOMoves.push(index);
        }

        playerX = !playerX;

        if (!playerX) {
            setTimeout(computerMove, 500);
        }
    };

    const computerMove = () => {
        const bestMove = minimax(squares, 0, true).index;
        handleClick(bestMove);
    };

    const minimax = (board, depth, isMaximizing) => {
        const winner = calculateWinner(board);
        if (winner === "X") return { score: -10 };
        if (winner === "O") return { score: 10 };
        if (board.every((square) => square !== null)) return { score: 0 };

        const moves = [];

        for (let i = 0; i < 9; i++) {
            if (board[i] === null) {
                const move = {};
                move.index = i;
                board[i] = isMaximizing ? "O" : "X";

                const result = minimax(board, depth + 1, !isMaximizing);
                move.score = result.score;

                board[i] = null;
                moves.push(move);
            }
        }

        let bestMove;
        if (isMaximizing) {
            let bestScore = -Infinity;
            for (const move of moves) {
                if (move.score > bestScore) {
                    bestScore = move.score;
                    bestMove = move;
                }
            }
        } else {
            let bestScore = Infinity;
            for (const move of moves) {
                if (move.score < bestScore) {
                    bestScore = move.score;
                    bestMove = move;
                }
            }
        }

        return bestMove;
    };

    function calculateWinner(squares) {
        const lines = [
            [0, 1, 2],
            [3, 4, 5],
            [6, 7, 8],
            [0, 3, 6],
            [1, 4, 7],
            [2, 5, 8],
            [0, 4, 8],
            [2, 4, 6],
        ];

        for (const [a, b, c] of lines) {
            if (
                squares[a] &&
                squares[a] === squares[b] &&
                squares[a] === squares[c]
            ) {
                return squares[a];
            }
        }
        return null;
    }

    function resetGame() {
        squares = Array(9).fill(null);
        playerX = true;
        playerXMoves = [];
        playerOMoves = [];
        xCounter = 0;
        oCounter = 0;
    }
</script>

<main>
    <h1>
        {#if calculateWinner(squares)}
            Winner: {calculateWinner(squares)}
            <br />
            <button onclick={resetGame}>Play Again</button>
            <br />
        {:else}
            Next Player: {playerX ? "X" : "O"}
        {/if}
    </h1>
    <div class="board">
        {#each squares as square, index}
            <button class="square" onclick={() => handleClick(index)}>
                <span class={square === "X" ? "x" : square === "O" ? "o" : ""}>
                    {square}
                </span>
            </button>
        {/each}
    </div>

    <br /><br /><br /><br /><br />

    <a href="/">Homepage</a>
    <br /><br />
    <a href="https://github.com/savashn/tic-tac-toe">Visit on Github</a>
</main>
