<template>
<section>
    <div class="container py-5 h-100">
        <div class="row d-flex justify-content-center align-items-center h-100">
            <div class="col-md-12 col-xl-10 pt-5">
                <div class="card">
                <div class="card-body">
                    <table class="table mb-0">
                        <thead>
                            <tr>
                            <th scope="col">Team Member</th>
                            <th scope="col">Task</th>
                            <th scope="col">Priority</th>
                            <th scope="col">Actions</th>
                            </tr>
                        </thead>
                        <tbody>
                            <TodoItem 
                                v-for="todo in todos" 
                                :key="todo.id" 
                                :todoProps="todo"
                                @item-completed="markComplete"
                                @item-deleted="deleteItem"
                            />
                        </tbody>
                    </table>
                </div>
                <div class="card-footer text-end p-3">
                    <button class="me-2 btn btn-link">Cancel</button>
                    <button class="btn-add">Add Task</button>
                </div>
                </div>

            </div>
        </div>
    </div>
</section>
</template>

<script>

import { ref } from 'vue'
import TodoItem from './TodoItem'

export default {
    name: 'ToDos',
        components: { TodoItem },
    setup() { // truyền toàn bộ dữ liệu cho compnent
        const todos = ref([
            {
                id: "1",
                teamMember: {
                    avatar: "https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-chat/ava2-bg.webp",
                    name: "Alice Mayer"
                },
                task: "Call Sam For payments",
                priority: "High priority",
                completed: false
            },
            {
                id: "2",
                teamMember: {
                    avatar: "https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-chat/ava1-bg.webp",
                    name: "John Smith"
                },
                task: "Send project proposal to client",
                priority: "Low priority",
                completed: false
            },
            {
                id: "3",
                teamMember: {
                    avatar: "https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-chat/ava3-bg.webp",
                    name: "Emily Johnson",
                },
                task: "Prepare sales presentation",
                priority: "Low priority",
                completed: false
            },
            {
                id: "4",
                teamMember: {
                    avatar: "https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-chat/ava4-bg.webp",
                    name: "Michael Wilson"
                },
                task: "Review website redesign mockups",
                priority: "Middle priority",
                completed: false
            },
            {
                id: "5",
                teamMember: {
                    avatar: "https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-chat/ava5-bg.webp",
                    name: "Sophia Davis"
                },
                task: "Schedule team meeting",
                priority: "Low priority",
                completed: true
            }
        ])

        const markComplete = (id) => {
            todos.value = todos.value.map(todo => {
                if(todo.id === id) todo.completed = !todo.completed
                return todo
            })
        }

        const deleteItem = (id) => {
            todos.value = todos.value.filter(todo => {
                return todo.id !== id
            });
        };

        return { 
            todos,
            markComplete,
            deleteItem
        } 
    },
}
</script>

<style>

.card {
    border-radius: 10px;
}
.checked {
    fill:#14a44d;
}

.deleted {
    fill: #dc4c64;
}

.btn-add:hover {
    opacity: 0.9;
}

.btn-add {
    padding: 6px;
    border-radius: 10px;
    border: none;
    color: #fff;
    background: linear-gradient(to right, rgba(126, 64, 246, 1), rgba(80, 139, 252, 1));
}
</style>