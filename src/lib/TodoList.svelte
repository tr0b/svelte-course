<svelte:options immutable={true}/>

<script>
    import Button from './Button.svelte';
    import { createEventDispatcher } from 'svelte';

    export let todos = [];
    let inputText = '';

    const dispatch = createEventDispatcher();

    function handleAddTodo() {
        dispatch(
            'addtodo',
            {
                title: inputText
            },
            { cancelable: true }
        );
        inputText = '';
    }

    function handleRemoveTodo(id) {
        dispatch('removetodo', {
            id
        })
    }


    function handleToggleTodo(id, completed) {
        dispatch('toggletodo', {
            id,
            completed,
        })
    }

</script>

<div class="todo-list-wrapper">
    <ul>
        {#each todos as { id, title, completed } (id)}
            <li>
                <label>
                    <input type="checkbox" checked={completed} on:input={(event) => {
                        event.currentTarget.checked = completed;
                        handleToggleTodo(id, !completed);
                    }} />
                    {title}
                </label>
                <button on:click={() => handleRemoveTodo(id)}>Remove</button>
            </li>
        {/each}
    </ul>

    <form class="add-todo-form" on:submit|preventDefault={handleAddTodo}>
        <input bind:value={inputText} />
        <Button
            type="submit"
            size="small"
            shadow
            bgColor="red"
            textColor="white">Add</Button
        >
    </form>
</div>
