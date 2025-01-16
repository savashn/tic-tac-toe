<script>
    let { children } = $props();
</script>

{@render children()}

<style>
    :global(body) {
        margin: 0;
        padding: 0;
        line-height: 1;
        background-color: black;
        color: white;
        height: 100vh;
        font-family: Arial, sans-serif;
    }

    :global(main) {
        text-align: center;
        margin-top: 5rem;
    }

    :global(a) {
        color: white;
        font-size: 1.5rem;
    }

    :global(.board) {
        display: grid;
        grid-template-columns: repeat(3, 8rem);
        gap: 5px;
        justify-content: center;
        margin-top: 5rem;
    }

    :global(.square) {
        width: 8rem;
        height: 8rem;
        font-size: 2rem;
        text-align: center;
        background-color: gray;
    }

    :global(.x) {
        font-size: 6rem;
        animation: drawX 1s ease-in-out forwards;
        color: red;
    }

    :global(.o) {
        font-size: 6rem;
        animation: drawO 1s ease-in-out forwards;
        color: blue;
    }

    @media (max-width: 768px) {
        :global(.board) {
            grid-template-columns: repeat(3, 6rem);
        }

        :global(.square) {
            width: 6rem;
            height: 6rem;
        }

        :global(.x) {
            font-size: 5rem;
        }

        :global(.o) {
            font-size: 5rem;
        }
    }

    @keyframes -global-drawX {
        0% {
            transform: scale(0);
            opacity: 0;
        }
        50% {
            transform: scale(1.1);
            opacity: 1;
        }
        100% {
            transform: scale(1);
            opacity: 1;
        }
    }

    @keyframes -global-drawO {
        0% {
            transform: scale(0);
            opacity: 0;
            border-radius: 50%;
        }
        50% {
            transform: scale(1.1);
            opacity: 1;
            border-radius: 50%;
        }
        100% {
            transform: scale(1);
            opacity: 1;
            border-radius: 50%;
        }
    }
</style>
