<template>
    <tr :class="['fw-normal', todoProps.completed ? 'is-completed' : '' ]">
        <th> 
            <img :src="todoProps.teamMember.avatar"
                class="shadow-1-strong rounded-circle" alt="avatar 1"
                style="width: 55px; height: auto;">
            <span class="ms-2">{{ todoProps.teamMember.name }}</span>
        </th>
        <td class="align-middle  ">
            <span>{{ todoProps.task }}</span>
        </td>
        <td class="align-middle">
            <h6 class="mb-0">
                <span 
                    :class="['badge', todoProps.priority === 'Low priority' ? 
                    'bg-low' : ( todoProps.priority === 'High priority' ? 'bg-high' : 'bg-middle')]"
                >
                    {{todoProps.priority}}
                </span>
            </h6>
        </td>
        <td class="align-middle">
            <a href="#" data-mdb-toggle="tooltip" title="Done"
                @click="markItemCompleted"
            >
                <i class="me-3">
                    <svg class="checked" xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 448 512">
                    <path d="M438.6 105.4c12.5 12.5 12.5 32.8 0 45.3l-256 256c-12.5 12.5-32.8 12.5-45.3 0l-128-128c-12.5-12.5-12.5-32.8 0-45.3s32.8-12.5 45.3 0L160 338.7 393.4 105.4c12.5-12.5 32.8-12.5 45.3 0z"/></svg>
                </i>
            </a>
            <a href="#" data-mdb-toggle="tooltip" title="Remove"
                @click="deleteItem"
            >
                <svg class="deleted" xmlns="http://www.w3.org/2000/svg" height="1em" viewBox="0 0 448 512">
                <path d="M170.5 51.6L151.5 80h145l-19-28.4c-1.5-2.2-4-3.6-6.7-3.6H177.1c-2.7 0-5.2 1.3-6.7 3.6zm147-26.6L354.2 80H368h48 8c13.3 0 24 10.7 24 24s-10.7 24-24 24h-8V432c0 44.2-35.8 80-80 80H112c-44.2 0-80-35.8-80-80V128H24c-13.3 0-24-10.7-24-24S10.7 80 24 80h8H80 93.8l36.7-55.1C140.9 9.4 158.4 0 177.1 0h93.7c18.7 0 36.2 9.4 46.6 24.9zM80 128V432c0 17.7 14.3 32 32 32H336c17.7 0 32-14.3 32-32V128H80zm80 64V400c0 8.8-7.2 16-16 16s-16-7.2-16-16V192c0-8.8 7.2-16 16-16s16 7.2 16 16zm80 0V400c0 8.8-7.2 16-16 16s-16-7.2-16-16V192c0-8.8 7.2-16 16-16s16 7.2 16 16zm80 0V400c0 8.8-7.2 16-16 16s-16-7.2-16-16V192c0-8.8 7.2-16 16-16s16 7.2 16 16z"/></svg>
            </a>
        </td>
    </tr>
</template>

<script>

export default {
    name: "ToDoItem",
    props: ['todoProps'],
    setup(props, context) {
        const markItemCompleted = () => {
            context.emit('item-completed', props.todoProps)
        }

        const deleteItem = () => {
            context.emit('item-deleted', props.todoProps.id)
        }
        
        return {
            markItemCompleted,
            deleteItem
        }
    }
}
</script>

<style>
.is-completed {
    text-decoration: line-through;
}

.bg-high {
    background-color: #dc4c64;
}

.bg-low {
    background-color: #14a44d;
}

.bg-middle {
    background-color: #e4a11b;
}
</style>