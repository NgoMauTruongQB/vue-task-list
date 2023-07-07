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
                <div class="card-footer p-5">
                    <AddToDo
                        @add-item="addItem"
                    />
                </div>
                <!-- <div class="card-footer text-end p-3">
                    <button class="me-2 btn btn-link">Cancel</button>
                    <button class="btn-add">Add Task</button>
                </div> -->
                </div>

            </div>
        </div>
    </div>
</section>
</template>

<script>

import { ref } from 'vue'
import TodoItem from './TodoItem'
import AddToDo from './AddToDo'
// import { v4 as uuidv4 } from 'uuid'
import axios from 'axios'

export default {
    name: 'ToDos',
        components: { TodoItem, AddToDo },
    setup() { // Get all data for component
        const todos = ref([])

        // get all data from API
        const getAllTodos = async () => {
            try {
                const res = axios.get('http://localhost:3000/todos')
                todos.value = (await res).data
            } catch (error) {
                console.log(error)
            }
        }
        getAllTodos()

        // const markComplete = (id) => {
        //     todos.value = todos.value.map(todo => {
        //         if(todo.id === id) todo.completed = !todo.completed
        //         return todo
        //     })
        // }
        
        // update todo
        const markComplete = async (todo) => {
            try {
                const response = await axios.patch(`http://localhost:3000/todos/${todo.id}`, { completed: !todo.completed });
                if (response.status >= 200 && response.status < 300) {
                    todos.value = todos.value.map(existingTodo => {
                        if (existingTodo.id === todo.id) {
                            return { ...existingTodo, completed: !todo.completed };
                        }
                        return existingTodo;
                    })
                } else {
                    console.log(`Error: Todo completion status update failed.`);
                }
            } catch (error) {
                console.log(error);
            }
        }

        // delete todo
        const deleteItem = async (id) => {
            try {
                await axios.delete(`http://localhost:3000/todos/${id}`)
                todos.value = todos.value.filter(todo => { todo.id !== id })
                getAllTodos()
            } catch (error) {
                console.log(error)
            }
        }

        // insert todo
        const addItem = async (newItem) => {
            try {
                const res = await axios.post('http://localhost:3000/todos', newItem)
                todos.value.push(res.data)
            } catch (error) {
                console.log(error)
            }
        }

        // only return when you want to pass data for component
        return { 
            todos,
            markComplete,
            deleteItem,
            addItem
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