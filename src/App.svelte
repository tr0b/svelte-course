<script>
    import TodoList from './lib/TodoList.svelte';
    import { v4 as uuid } from 'uuid';
    let todos = [
        {
            id: uuid(),
            title: 'Todo 1',
            completed: true
        },
        {
            id: uuid(),
            title: 'Todo 2',
            completed: true
        },
        {
            id: uuid(),
            title: 'Todo 3',
            completed: false
        },
        {
            id: uuid(),
            title: 'Todo 4',
            completed: true
        }
    ];

    function handleAddTodo(event) {
        todos = [
            ...todos,
            {
                id: uuid(),
                title: event?.detail?.title,
                completed: false
            }
        ];
    }

    function handleRemoveTodo({ detail }) {
        todos = todos.filter(({ id }) => id !== detail?.id);
    }

    function handleToggleTodo({ detail }) {
        const { completed } = detail;
        todos = todos.map((todo) => {
            if (detail?.id !== todo.id) {
                return todo;
            }
            return { ...todo, completed };
        });
    }
</script>

<TodoList {todos} on:addtodo={handleAddTodo} on:removetodo={handleRemoveTodo} on:toggletodo={handleToggleTodo} />

<style>
</style>
