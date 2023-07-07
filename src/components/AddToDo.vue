<template>
    <form @submit="addItem">
        <div class="mb-3">
            <label for="member" class="form-label">Team Member</label>
            <input type="text" class="form-control" aria-describedby="Member name"
                v-model="member"
            >
        </div>
        <div class="mb-3">
            <label for="task" class="form-label">Task</label>
            <input type="text" class="form-control"
                v-model="task"
            >
        </div>
        <div class="mb-3">
            <label for="priority" class="form-label">Priority</label>
            <select class="form-select"
                v-model="priority"
            >
                <option value="High priority">High priority</option>
                <option value="Middle priority">Middle priority</option>
                <option value="Low priority">Low priority</option>
            </select>
        </div>
        <button type="submit" class="btn-submit">Submit</button>
    </form>
</template>

<script>
import { ref } from 'vue'

export default {
    name: 'AddToDo',
    setup(props, context) {
        const member = ref('')
        const priority = ref('')
        const task = ref('')

        const addItem = (event) => {
            event.preventDefault()

            const newItem = {
                teamMember: {
                    avatar: "https://haycafe.vn/wp-content/uploads/2022/02/Avatar-trang-den.png",
                    name: member.value
                },
                task: task.value,
                priority: priority.value,
                completed: false
            }
            context.emit('add-item', newItem)

            member.value = ''
            task.value = ''
        }
        return {
            member,
            task,
            priority,
            addItem,
        }
    },
}
</script>

<style scoped>
    .btn-submit {
        padding: 6px;
        border-radius: 10px;
        border: none;
        color: #fff;
        background: linear-gradient(to right, rgba(126, 64, 246, 1), rgba(80, 139, 252, 1));
    }
</style>