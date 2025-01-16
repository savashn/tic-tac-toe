<div class="homepage">
    <button class="btn">
        <a href="/computer">Play against computer</a>
    </button>
    <br />
    OR
    <br />
    <br />
    <button class="btn">
        <a href="/player">Play against player</a>
    </button>

    <br /><br /><br /><br /><br />

    <a href="/">Homepage</a>
    <br />
    <a href="https://github.com/savashn/tic-tac-toe">Visit on Github</a>
</div>

<style>
    .homepage {
        margin-top: 20rem;
        display: grid;
        gap: 10px;
        text-align: center;
    }

    .btn {
        border: 1px solid rgb(15, 15, 223);
        background-color: transparent;
        padding: 10px;
        color: white;
        width: fit-content;
        place-items: center;
        margin: auto;
    }

    a {
        color: white;
        text-decoration: none;
        font-size: 3rem;
        font-family: Arial, Helvetica, sans-serif;
    }

    @media (max-width: 768px) {
        .homepage {
            margin-top: 15rem;
        }

        a {
            font-size: 2rem;
        }
    }
</style>
