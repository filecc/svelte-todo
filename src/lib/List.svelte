<script>
    export let list = [];
    import { createEventDispatcher } from 'svelte';

	const dispatch = createEventDispatcher();

    function requestToDelete(id) {
        dispatch('id', {
            id: id
        })  
        
       
    }
</script>

{#if list.length > 0}
<ul class="max-w-lg">
    {#each list as element}
    <li class="flex justify-between items-center gap-6">
        <span>{element.text}</span>
        <button on:click={() => requestToDelete(element.id)} class="text-red-600 underline">Delete</button>
    </li>
    {/each}
</ul>
{:else}
<p>La tua lista &egrave; vuota.</p>

{/if}
