
<script lang="ts">
    import { onMount } from "svelte";
    import * as wasm from "$lib/pkg";

    let rustFn: (arg0: string) => string;
    let test: string = "";

    onMount(async () => {
        await wasm.default();
        wasm.greet("WASM");

        rustFn = wasm.process_json;
    });
</script>


<h1>Welcome to SvelteKit</h1>

<button on:click={() => test = rustFn("my string")}>
    Knock it off
</button>

{#if (test)}
    <h3>{test}</h3>
{/if}