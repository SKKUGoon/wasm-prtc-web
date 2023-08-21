
<script lang="ts">
    import * as WXLS from "$lib/wxls/wxls";
    import { onMount } from "svelte";

    let myCell1: WXLS.Cell;
    let myCell2: WXLS.Cell;
    let myCell3: WXLS.Cell;
    let myRange: WXLS.Range;

    let hasResultCell2: boolean;
    let hasResultCell3: boolean;

    // For dramatic purpose
    let button1 = false;
    let button2 = false;
    let button3 = false;
    let button4 = false;

    onMount(async() => {
        // Svelte components are expected to initialize synchronously.
        // Even if I called `await WXLS.default()` at the top, it would have unexpected result.
        // Even if top-level `await` were supported, it could cause component to hand during the initialization util the WebAssembly module is loaded. 
        console.log("calling WASM");
        await WXLS.default();
        console.log("called WASM)");

        myCell1 = new WXLS.Cell(0, 0, undefined);
        myCell2 = new WXLS.Cell(1, 1, undefined);
        myCell3 = new WXLS.Cell(1, 5, "Sheet1");

        myRange = new WXLS.Range(myCell1, myCell2);

        hasResultCell2 = myRange.has(myCell2);
        hasResultCell3 = myRange.has(myCell3);
    })
</script>


<h1>Welcome to SvelteKit</h1>

<button on:click={() => button1 = true}>
    Turn `myCell1` into string address.
</button>

{#if (button1)}
    <h3>myCell1's string address is {myCell1.to_str_address()}</h3>
{/if}

<button on:click={() => button2 = true}>
    How about `myCell2` and `myCell3`
</button>

{#if (button2)}
    <h3>myCell2 = {myCell2.to_str_address()} and myCell3 = {myCell3.to_str_address()}</h3>
{/if}

<button on:click={() => button3 = true}>
    Let's see about range
</button>
{#if (button3)}
    <h3>Range is? {myRange.to_str_address()}. Tadah</h3>
{/if}

<button on:click={() => button4 = true}>
    Does Range has Cell2, and Cell3
</button>

{#if (button4)}
    <h3>Cell2 {hasResultCell2}</h3>
    <h3>Cell3 {hasResultCell3}</h3>
{/if}