<script lang="ts">
    import Quiz from "./lib/Quiz.svelte";
    import UTBLogo from "/utb.svg";
</script>

<header>
    <a href="https://www.underthebutton.com/">
        <img src={UTBLogo} alt="Under the Button Logo" />
        <h1>under the <b>button</b></h1>
    </a>
</header>

<main>
    <Quiz />
</main>

<style lang="scss">
    header {
        text-align: center;
        img {
            height: 6em;
            will-change: filter;
            transition: filter 300ms;
            filter: drop-shadow(0 0 5px gray);

            &:hover {
                filter: drop-shadow(0 0 10px gray);
            }
        }
        h1 {
            b {
                color: $blue;
                font-weight: 600;
            }
        }
    }
    main {
        margin-bottom: 40vh;
    }
</style>
