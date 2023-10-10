<script>
  import List from "./lib/List.svelte";

  $: list = [...JSON.parse(localStorage.getItem('list'))] || []
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


</script>

<main>
  <h1 class="text-center text-2xl p-6">A simple Todo with Svelte</h1>
  
  <div class="grid place-items-center p-6">
    <div class="flex gap-2 items-stretch">
      <input on:keydown={(e) => keydown(e)} class="rounded p-3 border-2 border-slate-400" type="text" bind:value={text}>
      <button on:click={handleAdd} class="px-2 bg-green-600 text-white rounded border-2 border-green-500 hover:bg-green-400 hover:border-green-300 transition-colors duration-500 cursor-pointer">Add</button>
    </div>
  </div>

<div class="text-center">
  <List {list} />
</div>
  
</main>

<style>
 
</style>
