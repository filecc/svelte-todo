<script>
    export let list = [];
</script>

{#if list.length > 0}
<ul>
    {#each list as element}
    <li>{element.text}</li>
    {/each}
</ul>
{:else}
<p>La tua lista &egrave; vuota.</p>

{/if}
