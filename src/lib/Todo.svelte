<script>
  import { createEventDispatcher } from "svelte";
  const dispatch = createEventDispatcher();
  //PROPS
  export let todo;

  function handleComplete(e, id) {
    dispatch("complete", {
      isCompleted: e.target.checked,
      id: id
    });
  }

  function handleDelete(id) {
    dispatch("delete", {
      id: id
    });
  }
</script>

<li>
  <span class={todo.isCompleted ? "completed" : "falopa"}>{todo.task}</span>
  <div class="todo-control">
    <input
      on:change={(e) => handleComplete(e, todo.id)}
      type="checkbox"
      checked={todo.isCompleted}
    />
    <button on:click={() => handleDelete(todo.id)}><i class="fa-solid fa-trash-can" /></button>
  </div>
</li>

<style lang="scss">
  li {
    list-style-type: none;
    display: flex;
    align-items: center;
    margin: 10px 0px;
    width: 500px;

    .todo-control {
      display: flex;
      margin-left: 25px;
      gap: 10px;

      input {
        cursor: pointer;
      }
    }

    span {
      display: block;
      width: 500px;
      word-break: break-word;

      &.completed {
        text-decoration: line-through;
      }
    }
  }
  button {
    border: none;
    padding: 5px 10px;
    cursor: pointer;
    background-color: transparent;
  }
</style>
