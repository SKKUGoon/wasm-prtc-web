
<script lang="ts">
    import { onMount } from "svelte";
    import * as wasm from "$lib/pkg";

    let rustFn: (arg0: string) => string;
    let rustCls: wasm.Foo;
    let test: string = "";
    let structTest: string = "";

    const handleClick = async () => {
        if (rustCls) {
            structTest = rustCls.bar();
        }
    }

    onMount(async () => {
        await wasm.default();
        wasm.greet("WASM");

        rustFn = wasm.process_json;
        rustCls = wasm.Foo.new("my foo string");
    });
</script>


<h1>Welcome to SvelteKit</h1>

<button on:click={() => test = rustFn("my string")}>
    Knock it off
</button>

{#if (test)}
    <h3>{test}</h3>
{/if}

<button on:click={handleClick}>
    Duck you too
</button>

{#if (structTest)}
    <h3>{structTest}</h3>
{/if}