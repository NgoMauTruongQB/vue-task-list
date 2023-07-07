<template>
    <header class="header">
        <nav class="navbar fixed-top" style="background-color: #fff;">
            <div class="d-flex justify-content-center">
                <img src="https://mdbcdn.b-cdn.net/img/Photos/new-templates/bootstrap-todo-list/check1.webp" alt="Check" width="50" class="m-1"/>
                <h2 style="height: 50;  color: blue" class="m-1">Task List</h2>
            </div>
        </nav>
        
    </header>
</template>

<script>
export default {
  name: "PageHeader",
};
</script>

<style scoped>
.navbar {
    box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
}
</style>