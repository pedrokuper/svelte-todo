<script>
  import TodoList from "./lib/TodoList.svelte";
  let todos = [];
  let task = "";
  let timer;

  function handleTodos(e) {
    const { value } = e.target;
    //Debouncer
    clearTimeout(timer);
    timer = setTimeout(() => {
      task = value;
    }, 500);
  }

  function addTodo() {
    if (task.trim() === "") return;
    const newTodo = {
      task,
      isCompleted: false,
      id: Date.now()
    };
    todos = [...todos, newTodo];
    task = "";
    clearTimeout(timer);
  }

  function handleMessage(event) {
    const { isCompleted, id } = event.detail;

    const updatedTodos = todos.map((todo) => {
      if (todo.id === id) {
        return { ...todo, isCompleted };
      }
      return todo;
    });

    todos = updatedTodos;
  }

  function handleDelete(e) {
    const { id } = e.detail;
    todos = todos.filter((todo) => {
      return todo.id !== id;
    });
  }
</script>

<section>
  <header>
    <h1>Todo List</h1>
  </header>

  <form on:submit|preventDefault={addTodo} action="">
    <label for="todo"
      >Agregar tareas
      <input bind:value={task} type="text" name="todo" id="todo" on:input={handleTodos} />
    </label>
    <button>Agregar</button>
  </form>

  <TodoList on:complete={handleMessage} on:delete={handleDelete} {todos} />
</section>

<style lang="scss">
  h1 {
    text-align: center;
  }
  input {
    width: 500px;
    border: 1px solid black;
    height: 20px;

    &:focus {
      outline: 3px solid greenyellow;
      border: none;
    }
  }

  section {
    display: flex;
    flex-direction: column;
    align-items: center;
  }
</style>
