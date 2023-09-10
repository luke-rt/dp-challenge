<script lang="ts">
    import data from "../assets/data.json";
    import Question from "./Question.svelte";

    let responses: number[] = [];
    let result: string = "";

    const handleSubmit = (responses: number[]) => {
        // already assumes an option has been given for all since the submit button is disabled otherwise
        let counts = Array(data.results.length).fill(0);
        let maxCount = 0;
        let maxOption;
        for(let e of responses) {
            counts[e]++;

            if(counts[e] > maxCount) {
                maxCount = counts[e];
                maxOption = e;
            }
        }
        
        result = data.results[maxOption];
    }

    const handleRetake = () => {
        responses = [];
        result = "";
    }
</script>

<section>
    {#each data.questions as question, i}
        <Question
            {question}
            index={i}
            bind:response={responses[i]}
            disabled={result != ""}
        />
    {/each}
</section>

<section class="submit-retake">
    {#if result == ""}
        <button disabled={responses.includes(-1)} on:click={() => handleSubmit(responses)}>
            Show me my results!
        </button>
    {:else}
        <a href="/">
            <button on:click={handleRetake}>
                I want to retake!
            </button>
        </a>
    {/if}
</section>

{#if result}
    <section class="result">
        {result}
    </section>
{/if}

<style lang="scss">
    .submit-retake {
        button {
            width: 220px;
            margin: 40px auto;
            display: block;
            padding: 30px;

            font-size: 1.1em;
            text-align: left;

            border: none;
            border-radius: 5px;

            color: white;
            background-color: $blue;

            box-shadow: 3px 3px 10px lightgray;

            &:hover {
                cursor: pointer;
                box-shadow: 3px 3px 10px lightgray;
                transition: 0.25s;
            }

            &:disabled {
                color: whitesmoke;
                background-color: gray;
                cursor: not-allowed;
            }
        }
    }
    .result {
        padding: 30px;
        background-color: lightgray;

        border: 2px solid gray;
        border-radius: 5px;

        margin-block: 8vh;
    }
</style>
