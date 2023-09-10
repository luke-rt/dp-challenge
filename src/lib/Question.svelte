<script lang="ts">
    export let question;
    export let index;
    export let disabled = false;

    export let response = -1;
</script>

<p class:hi = {true}>{index+1}. {question.prompt}</p>
{#each Object.values(question.options) as opt, i}
    <button
        on:click={() => {response = i}}
        class:clicked={response === i}
        {disabled}
    >
        {String.fromCharCode(i + 1 + 64)}
        . 
        {opt}
    </button>
{/each}

<style lang="scss">
    p {
        margin-top: 12vh;
        font-weight: bolder;
    }
    button {
        display: block;
        width: 100%;
        margin-block: 15px;
        padding: 20px 10px;

        font-size: 1.1em;
        text-align: left;

        border: none;
        border-radius: 5px;

        transition: 0.25s;

        &:hover {
            cursor: pointer;
            box-shadow: 3px 3px 10px lightgray;
        }

        &:active {
            transform: scale(.95);
        }

        &.clicked {
            color: white;
            background-color: $blue;
            box-shadow: 3px 3px 10px gray;
            transition: 0.5s;
        }
    }
</style>
