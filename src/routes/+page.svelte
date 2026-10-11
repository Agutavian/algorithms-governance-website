<!--FROM: https://svelte.dev/playground/a9a5a1639103474f9f215a3bbbc40bc9?version=5.57.2-->
<script lang="ts">
    import {writable } from 'svelte/store'
    import { onMount } from 'svelte';

    let metaAlgorithms = $state(0)
    let googleSearches = $state(0)
    let openAIPrompts = $state(0)
    let usTransactions = $state(0)

    let metaAlgorithmsDerived = $derived(metaAlgorithms.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ","))
    let googleSearchesDerived = $derived(googleSearches.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ","))
    let openAIPromptsDerived = $derived(openAIPrompts.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ","))
    let usTransactionsDerived = $derived(usTransactions.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ","))

    onMount(() => {

        // 6,000,000 a second
        const intervalMeta = setInterval(() => {
            increaseMeta(6000)
        }, 1);

        // 3.5 billion a day (2017), outdated
        // const intervalGoogle = setInterval(() => {
        //     increaseGoogle(40)
        // }, 1);

        // 16 billion a day, 185,815 per second, 185/milsecond
        // Source: https://www.demandsage.com/google-search-statistics/
        const intervalGoogle = setInterval(() => {
            increaseGoogle(185)
        }, 1);

        // 2 billion prompts a day, 23,150 per second, 23.15/milsecond
        // Source: https://www.independent.co.uk/tech/chatgpt-openai-daily-users-prompts-b2793502.html
        const intervalOpenAI = setInterval(() => {
            increaseOpenAI(23)
        }, 1);

        // 165,019,944 a day, 1,910 per second, 23.15/milsecond
        // Source: https://capitaloneshopping.com/research/number-of-credit-card-transactions/
        const usTransactions = setInterval(() => {
            increaseUSTransactions(2)
        }, 1);

        return () => {
            clearInterval(intervalMeta)
            clearInterval(intervalGoogle)
        };
    })


    function increaseMeta(increaseAmount: number) {
        console.log(increaseAmount)
        metaAlgorithms += increaseAmount
    }
    function increaseGoogle(increaseAmount: number) {
        console.log(increaseAmount)
        googleSearches += increaseAmount
    }
    function increaseOpenAI(increaseAmount: number) {
        console.log(increaseAmount)
        openAIPrompts += increaseAmount
    }
    function increaseUSTransactions(increaseAmount: number) {
        console.log(increaseAmount)
        usTransactions += increaseAmount
    }
</script>

<!--<h1>-->
<!--    Since the opening of this page:-->
<!--</h1>-->
<div class="outermost-body">
    <div class="body">
        <div class="prediction-container in-paper">
            <div class="text-container">
                <h3>
                    {metaAlgorithmsDerived}
                </h3>

                <div class="bottom-text">
                    <p>
                        Meta Predictions
                    </p>
                    <p class="tiny">
                        (6,000,000/s)
                    </p>
                </div>
            </div>

        </div>

        <div class="prediction-container in-paper">
            <div class="text-container">
                <h3>
                    {googleSearchesDerived}
                </h3>
                <div class="bottom-text">
                    <p>
                        Google Searches
                    </p>
                    <p class="tiny">
                        (~185,000/s)
                    </p>
                </div>

            </div>
        </div>


        <div class="prediction-container in-paper">
            <div class="text-container">
                <h3>
                    {openAIPromptsDerived}
                </h3>
                <div class="bottom-text">
                    <p>
                        OpenAI Prompts
                    </p>
                    <p class="tiny">
                        (~23,000/s)
                    </p>
                </div>

            </div>
        </div>

        <div class="prediction-container in-paper">
            <div class="text-container">
                <h3>
                    {usTransactionsDerived}
                </h3>
                <div class="bottom-text">
                    <p>
                        Credit Card Transactions (United States)
                    </p>
                    <p class="tiny">
                        (~1,900/s)
                    </p>
                </div>

            </div>
        </div>

    </div>
</div>




<style>

    html, body {
        background-color: red;
    }

    .outermost-body {
        /*from https://stackoverflow.com/questions/356809/best-way-to-center-a-div-on-a-page-vertically-and-horizontally*/
        padding: 15px;
        position: absolute;
        top: 50%;
        left: 50%;
        -ms-transform: translateX(-50%) translateY(-50%);
        -webkit-transform: translate(-50%,-50%);
        transform: translate(-50%,-50%);
        width: 100%;
    }
    .body {
        display: grid;
        grid-template-columns: auto auto auto auto;
        max-height: 100vh;
    }

    .prediction-container {
        border-radius: 10px;
    }
    .text-container {
        display: flex;
        flex-direction: column;
        gap: 5px;
        align-items: center;
        h3, p {
            margin: 0;
        }
        h3 {
            margin: 0;
            font-size: xxx-large;
        }
    }
    .bottom-text {
        display: flex;
        flex-direction: column;
        align-items: center;
        p {
            font-weight: 600;
        }
        .tiny {
            font-weight: 300;
            font-style: italic;
        }
    }
</style>