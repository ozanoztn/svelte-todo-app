<script>
	import { writable } from "svelte/store";

    export let todo;
    export let todos;

    let isModifying=false;

    function changeCheckState(){
        todo.Checked = !todo.Checked;
    }
    function changeIsModifyingState(){
        isModifying = !isModifying;
    }

    function removeTodoFromTodos(todo){
        todos.update(todos => todos.filter(t => t.Id !== todo.Id));
    }
</script>


<div class="todo" class:checked={todo.Checked}>
    {#if isModifying}
        <input type="text" bind:value={todo.TodoText}>
    {:else}
        {todo.TodoText}
    {/if}
    <div class="icons">
        <i class="fa-solid fa-pen" on:click={changeIsModifyingState}></i>
        <i class="fa-solid fa-trash" on:click={removeTodoFromTodos(todo)}></i>
        <i class="fa-solid fa-check" on:click={changeCheckState}></i>
    </div>
</div>


<style>

.todo{
    display: flex;
    justify-content: space-between;
    align-items: center;
    background-color: #7f78eb;
    color: white;
    width: 400px;
    padding: 1.5rem;
    font-size: 24px;
    border-radius: 8px;
    transition: all 150ms ease-in;
}

i{
    padding: 0.5rem;
    border-radius: 5px;
    transition: all 150ms ease-in;
}

.fa-pen:hover{
    background-color: #0f0e21;
    transition: all 150ms ease-in;
}

.fa-trash:hover{
    background-color: red;
    transition: all 150ms ease-in;
}
.fa-check:hover{
    background-color: green;
    transition: all 150ms ease-in;
}

.checked{
    text-decoration: line-through;
    background-color: limegreen;
    transition: all 150ms ease-in;
}
</style>