<script>
    export let list = [];
    import { IconArrowBack, IconCheck, IconPencil, IconTrash } from '@tabler/icons-svelte'
    let newText;
    $: editingId = null;
    import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

    function requestToDelete(id) {
        dispatch('delete', {
            id: id
        })  
    }

    function requestEdit()
    {
        dispatch('edit', {
            id: editingId,
            text: newText
        })
        newText = ''
        editingId = null
        
    }

    function edit(id){
        editingId = id
        newText = list[list.findIndex(element => element.id === id)].text
    }

    function keydown(event)
  {
    if (event.key === 'Enter')
    {
        requestEdit()
    }
  }
</script>

{#if list.length > 0}
<ul class="w-full p-3">
    {#each list as element}
    <li class="flex justify-between items-center gap-6 px-2 py-3 rounded bg-white mb-2 shadow-sm">
        {#if ( editingId === element.id)}
        <input autofocus class="rounded border-2 border-slate-400" type="text" bind:value={newText} on:keydown={(e) => keydown(e)}>
        {:else}
        <span>{element.text}</span>
        {/if}
       
        {#if editingId === element.id}
        <div>
            <button on:click={requestEdit} class="text-green-600 underline"><IconCheck size={24} stroke={2} /></button>
            <button on:click={() => editingId = null} class="text-yellow-600 underline"><IconArrowBack size={24} stroke={2} /></button>
        </div>
        
        {:else}
        <div>
            <button on:click={() => edit(element.id)} class="text-yellow-600 underline"><IconPencil size={24} stroke={2} /></button>
            <button on:click={() => requestToDelete(element.id)} class="text-red-600 underline"><IconTrash size={24} stroke={2} /></button>
        </div>
        
        {/if} 
    </li>
    {/each}
</ul>
{:else}
<p>You have nothing left to do.</p>

{/if}
