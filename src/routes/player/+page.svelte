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
