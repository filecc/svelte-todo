<script>
  import { IconPlus } from "@tabler/icons-svelte";
import List from "./lib/List.svelte";

  $: list = [...JSON.parse(localStorage.getItem('list')) || []]
  let text;


  function handleAdd() {
    let newTodo = {};
    newTodo.text = text
    newTodo.id = Date.now()
    list = [...list, newTodo]

    text = ''
    localStorage.setItem('list', JSON.stringify(list))
  }

  function keydown(event)
  {
    if (event.key === 'Enter')
    {
      handleAdd()
    }
  }

  function handleDelete(event)
  {
        const id = event.detail.id
   
        const toDelete = (element) => element.id === id;
        list.splice(list.findIndex(toDelete), 1)
        list = list
        localStorage.setItem('list', JSON.stringify(list))
  }

  function handleEdit(event)
  {
    const id = event.detail.id
    const newText = event.detail.text
    const toEdit = list.findIndex(element => element.id === id)
    
    list[toEdit].text = newText
    list = list
    localStorage.setItem('list', JSON.stringify(list))
  }

  function handleClearAll(){
    list = []
    list = list
    localStorage.removeItem('list')
  }

</script>

<main class="bg-slate-100 min-h-[100dvh] flex flex-col justify-center items-center">
  <h1 class="text-center text-2xl p-6">A simple Todo with Svelte</h1>
  
  <div class="grid place-items-center p-6">
    <div class="flex gap-2 items-stretch">
      <input on:keydown={(e) => keydown(e)} class="rounded p-3 border-2 border-slate-400" type="text" bind:value={text}>
      <button on:click={handleAdd} class="w-12 grid place-items-center bg-green-600 text-white rounded border-2 border-green-500 hover:bg-green-400 hover:border-green-300 transition-colors duration-500 cursor-pointer"><IconPlus size={24} stroke={2} /></button>
    </div>
  </div>

  <div class="text-center mb-6">
    {#if list.length > 0}
    <button class="px-2 py-1 bg-red-800 text-white rounded" on:click={handleClearAll}>Clear all the data</button>
    {/if}
  </div>
<div class="text-center grid place-items-center">
  <List on:edit={handleEdit} on:delete={handleDelete} {list} />
</div>
  
</main>

<style>
 
</style>
