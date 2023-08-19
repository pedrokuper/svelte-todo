<script>
  import { createEventDispatcher } from "svelte";
  import Todo from "./Todo.svelte";
  export let todos;
  const dispatch = createEventDispatcher();

  function forward(event) {
    dispatch("complete", event.detail);
  }

  function forwardDelete(e) {
    dispatch("delete", e.detail);
  }
</script>

<ul>
  {#each todos as todo}
    <Todo on:complete={forward} on:delete={forwardDelete} {todo} />
    <hr />
  {/each}
</ul>

<style>
  ul {
    padding: 0;
    padding: 10px 5px;
  }

  hr {
    margin: 15px 0px;
    width: 100%;
    border: 1px solid blue;
  }
</style>
