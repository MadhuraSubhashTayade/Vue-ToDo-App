<script setup>
const todos = defineProps({
    todos: {
        type: Array,
        required: true
    }
})
const emit = defineEmits(['delete-todo', 'edit-todo'])
const handleDelete = (id) => {
    emit('delete-todo', id)
}
const handleEdit = (id) => {
    emit('edit-todo', id)
}
</script>

<template>
    <div class="todo-container">
        <table>
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Name</th>
                    <th>Actions</th>
                </tr>
            </thead>
            <tbody v-for="(todo, index) in todos.todos" :key="index">
                <tr>
                    <td>{{ todo.id }}</td>
                    <td>{{ todo.name }}</td>
                    <td>
                        <button @click="() => handleEdit(todo.id)">Edit</button>
                        <button @click="() => handleDelete(todo.id)">Delete</button>
                    </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<style scoped>
.todo-container {
    width: 100%;
    margin: 0 auto;
    border: 2px solid #333;
    border-radius: 4px;
    overflow: hidden;
    font-family: sans-serif;
}

table {
    width: 100%;
    border-collapse: collapse;
    padding: 0 30px;
}

thead {
    background-color: #333;
    color: white;
}

th,
td {
    padding: 12px;
    text-align: left;
    border-bottom: 1px solid #ccc;
}

th:last-child {
    padding-right: 60px;
}

/* Right-align the last column (Actions) */
th:last-child,
td:last-child {
    text-align: right;
}

th:first-child,
td:first-child {
    padding-left: 20px;
}

tbody tr:nth-child(even) {
    background-color: #f2f2f2;
}

button {
    margin-right: 20px;
    padding: 4px 10px;
    border: none;
    background-color: rgb(25, 118, 210, 0.8);
    color: white;
    border-radius: 4px;
    cursor: pointer;
    font-size: 20px;
    text-transform: uppercase;
}

button:last-child {
    background-color: rgb(211, 47, 47, 0.8);
}
</style>
