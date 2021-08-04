<script>
    import {writable} from "svelte-local-storage-store";
    const todosStore = writable("todos", [{'done': false, 'text': 'random'}]);
    $: remaining = $todosStore.filter(t => !t.done).length;
    const add = () => $todosStore = $todosStore.concat({'done': false, 'text': ''})
    const clear = () => $todosStore = $todosStore.filter(t => !t.done)
</script>

<main style="background:white; color:black">
    <div style="display:grid; grid-gap: 25px; margin: 0 auto; max-width: 600px; padding:24px">
        <h1>Todos</h1>
        {#each $todosStore as todo}

            <div style="display: flex" class:done={todo.done}>
             
                <input class=""
                       type="text"
                       size="50"
                       placeholder="What needs to be done?"
                       bind:value={todo.text}
                >
                <input
                type=checkbox
                bind:checked={todo.done}
        >

            </div>
        {/each}

        <p>{remaining} remaining</p>

        <button on:click={add}>
            Add new
        </button>

        <button on:click={clear}>
            Clear completed
        </button>
    </div>
</main>

<style>
    h1 {
        text-align: center;
        font-size: 20px;
    }

    .done {
        opacity: 0.4;
    }

    input {
        border: none;
        border-bottom: 1px solid #2323;
        color: black;
        padding: 2px;
        /*background: gray;*/
    }
</style>