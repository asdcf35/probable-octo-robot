<script>
import { onMount } from "svelte";


	let todos = [];
	let todoText = [];
	
	onMount(()=>{
		const existingTodos = localStorage.getItem('todos');
		todos = JSON.parse(existingTodos) || [];
	})
	function addTodo(){
		todos = [...todos, todoText];
		localStorage.setItem('todos',JSON.stringify(todos));
		document.getElementById("todos3").value = '';
	}
	function removeTodo(todo){
		todos = todos.filter(e => e != todo);
	}
</script>
<main>
	<ul>
		{#each todos as todo}
			<li>{todo}</li>
			<button on:click={removeTodo(todo)}>X</button>
		{/each}
	</ul>

	<form on:submit|preventDefault={addTodo}>
		<input bind:value={todoText} id='todos3'>
		<input type="submit" value="Add todo" >
	</form>
</main>