<script>
    export let list = [];
    let newText;
    $: editingId = null;
    import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

    function requestToDelete(id) {
        dispatch('delete', {
            id: id
        })  
    }

    function requestEdit(id)
    {
        dispatch('edit', {
            id: id,
            text: newText
        })
        newText = ''
        editingId = null
        
    }

    function edit(id){
        newText = list[list.findIndex(element => element.id === id)].text
        editingId = id
    }

    function keydown(event)
  {
    if (event.key === 'Enter')
    {
        requestEdit(editingId)
    }
  }
</script>

{#if list.length > 0}
<ul class="max-w-lg">
    {#each list as element}
    <li class="flex justify-between items-center gap-6">
        {#if ( editingId === element.id)}
        <input class="rounded border-2 border-slate-400" type="text" bind:value={newText} on:keydown={(e) => keydown(e)}>
        {:else}
        <span>{element.text}</span>
        {/if}
       
        {#if editingId === element.id}
        <button on:click={() => requestEdit(element.id)} class="text-yellow-600 underline">Confirm</button>
        {:else}
        <button on:click={() => edit(element.id)} class="text-yellow-600 underline">Edit</button>
        {/if}
      
        <button on:click={() => requestToDelete(element.id)} class="text-red-600 underline">Delete</button>
        
    </li>
    {/each}
</ul>
{:else}
<p>La tua lista &egrave; vuota.</p>

{/if}
