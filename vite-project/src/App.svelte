<script>
	import { onMount, createEventDispatcher } from 'svelte';
  
	let todos = [];
	let newTodoText = '';
  
	const dispatch = createEventDispatcher();
  
	const addTodo = () => {
	  const newTodo = {
		id: Date.now(),
		text: newTodoText,
		completed: false
	  };
  
	  todos = [...todos, newTodo];
	  newTodoText = '';
	};
  
	const toggleTodo = (todo) => (todo.completed = !todo.completed, todos = [...todos]);

	const removeTodo = (id) => (dispatch('delete', { id }), todos = todos.filter((todo) => todo.id !== id));

	onMount(() => {
	  todos = [
		{ id: 1, text: 'Learn Svelte', completed: false },
		{ id: 2, text: 'Make money', completed: false },
		{ id: 3, text: 'Eat something', completed: false },
		{ id: 4, text: 'Crying in the shower', completed: false }
	  ];
	});
  </script>
  
  <div class="main-con">
	<h1>Mario's Todo App</h1>
  
	<div>
	  <input type="text" bind:value={newTodoText} placeholder="Add new todo" />
	  <button on:click={addTodo}>Add</button>
	</div>
  
	<div class="con">
	  {#each todos as todo (todo.id)}
		<div class="todo-item">
		  <input type="checkbox" checked={todo.completed} on:change={() => toggleTodo(todo)} />
		  <span class:completed={todo.completed}>{todo.text}</span>
		  <button on:click={() => removeTodo(todo.id)}>Delete</button>
		</div>
	  {/each}
	</div>
  </div>
	
<style>
	.con {
	  width: 250px;
	  display: flex;
	  flex-direction: column;
	  justify-content: space-around;
	  align-items: center;
	}
	
	.main-con {
	  width: 100%;
	  height: 100vh;
	  display: flex;
	  flex-direction: column;
	  justify-content: center;
	  align-items: center;
	}
	
	.todo-item {
	  width: 100%;
	  padding: 5px;
	  height: 50px;
	  display: flex;
	  justify-content: space-around;
	  align-items: center;
	  background-color: rgb(82, 82, 82);
	  border-radius: 5px;
	}
	
	.todo-item > input {
	  width: 20px;
	  height: 100%;
	}
	
	.todo-item > span {
	  width: 150px;
	  transform: translateY(-15%);
	}
	
	h1 {
	  margin-bottom: 16px;
	}
	
	input[type="text"] {
	  margin-right: 8px;
	}
	
	.todo-item {
	  margin-bottom: 8px;
	}
	
	.completed {
	  text-decoration: line-through;
	}
</style>
