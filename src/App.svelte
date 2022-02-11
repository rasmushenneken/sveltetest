<script>
  import { slide } from "svelte/transition"

  let name = "Rasmus"
  let newTodo = ""

  let todoId = 0

  let todos = [
    {
      id: ++todoId,
      title: "Buy kamil flowers",
      done: false,
    },
    {
      id: ++todoId,
      title: "Drink milk",
      done: true,
    },
    {
      id: ++todoId,
      title: "Play Phasmophobia with koozy and vinky",
      done: false,
    },
    {
      id: ++todoId,
      title: "Pray that my motorcycle is still ok",
      done: false,
    },
    {
      id: ++todoId,
      title: "Struggle with Svelte",
      done: true,
    },
  ]

  function addTodo() {
    if (newTodo === "") return

    todos = [
      {
        id: ++todoId,
        title: newTodo,
        done: false,
      },
      ...todos,
    ]

    newTodo = ""
  }

  function removeTodo(id) {
    todos = todos.filter(todo => todo.id !== id)
  }

  function clearCompleted() {
    todos = todos.filter(todo => !todo.done)
  }
</script>

<main>
  <h1>{name}, here are your tasks for today</h1>

  <section class="add-todo">
    <input type="text" placeholder="what to do?" bind:value={newTodo} />
    <button disabled={newTodo === ""} on:click={addTodo}>Add</button>
  </section>

  <section class="todos">
    {#each todos.filter(todo => !todo.done) as todo (todo.id)}
      <div transition:slide class="todo">
        <input type="checkbox" bind:checked={todo.done} name="complete task" />
        <input type="text" class:done={todo.done} bind:value={todo.title} />
        <button on:click={() => removeTodo(todo.id)}>x</button>
      </div>
    {/each}
    {#each todos.filter(todo => todo.done) as todo (todo.id)}
      <div transition:slide class="todo">
        <input type="checkbox" bind:checked={todo.done} name="complete task" />
        <input type="text" class:done={todo.done} bind:value={todo.title} />
        <button on:click={() => removeTodo(todo.id)}>x</button>
      </div>
    {/each}
  </section>

  <section>
    <button on:click={clearCompleted}>Clear completed</button>
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

  .todo input {
    border: none;
    background: lightpink;
    color: black;
  }
  .todo input.done {
    opacity: 0.5;
    text-decoration: line-through;
  }
</style>
