<script>
	import { writable } from "svelte/store";
import Todo from "../components/todo.svelte";
let todos = writable([]);
let input = "";

function AddTodoToList(event){
    if(event.key=='Enter'){
        let uniqueId = Math.random().toString(36).substr(2, 9);
        
        todos.update(todos => [...todos, {Id: uniqueId, TodoText: input, Checked: false}]);

        input="";
    }
}

</script>

<div class="container">

    <div class="addTodoContainer">
        <input type="text" placeholder="Todo" bind:value={input} on:keyup={AddTodoToList}>
    </div>

    <div class="todos">
        {#each $todos as todo (todo.Id)}
            <Todo todo={todo} todos={todos}></Todo>
        {/each}
    </div>

</div>


<style>
    :global(body) {
		margin: 0;
	}
    .container{
        width: 100%;
        height: 100vh;
        background-color: #0f0e21;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    .addTodoContainer{
        margin-top: 5rem;
        display: flex;
        justify-content: center;
        align-items: center;
    }
    .addTodoContainer input{
        width: 300px;
        height: 30px;
        border-radius: 5px;
        outline: 0;
        font-size: 24px;
        padding: 0.3rem;
    }
    .todos{
        margin-top: 25px;
        display: flex;
        flex-direction: column;
        gap: 25px;
    }
</style>