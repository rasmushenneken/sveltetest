<script>
  let name = "Rasmus"
  let newTodo = ""

  let todos = [
    {
      title: "Buy kamil flowers",
      done: false,
    },
    {
      title: "Drink milk",
      done: true,
    },
    {
      title: "Play Phasmophobia with koozy and vinky",
      done: false,
    },
    {
      title: "Pray that my motorcycle is still ok",
      done: false,
    },
    {
      title: "Struggle with Svelte",
      done: true,
    },
  ]

  function addTodo() {
    if (newTodo === "") return

    todos = [
      ...todos,
      {
        title: newTodo,
        done: false,
      },
    ]

    newTodo = ""
  }

  function removeTodo(i) {
    todos.splice(i, 1)
    todos = todos
  }
</script>

<main>
  <h1>{name}, here are your tasks for today</h1>

  <section class="add-todo">
    <input type="text" placeholder="what to do?" bind:value={newTodo} />
    <button disabled={newTodo === ""} on:click={addTodo}>Add</button>
  </section>

  <section class="todos">
    {#each todos as todo, i}
      <div class="todo">
        <input type="checkbox" bind:checked={todo.done} name="complete task" />
        <input type="text" disabled class:done={todo.done} value={todo.title} />
        <button on:click={() => removeTodo(i)}>x</button>
      </div>
    {/each}
  </section>
</main>

<style>
  main {
    display: grid;
    gap: 1rem;
  }
  .add-todo {
    display: grid;
    grid-template-columns: 1fr auto;
    gap: 0.5rem;
  }

  .todo {
    display: grid;
    grid-template-columns: auto 1fr auto;
    align-items: center;
    gap: 0.5rem;
  }

  input:disabled {
    border: none;
    background: lightpink;
    color: black;
  }
  input:disabled.done {
    opacity: 0.5;
    text-decoration: line-through;
  }
</style>
