<template>
    <div id="app">
        <PageHeader/>
        <ToDos/>
    </div>
</template>

<script>
import PageHeader from './components/PageHeader'
import ToDos from './components/ToDos'

export default {
    name: 'App',
    components: { PageHeader, ToDos }
}
</script>

<style>
#app {
    background: linear-gradient(to right, rgba(126, 64, 246, 1), rgba(80, 139, 252, 1));
    min-height: 100vh;
}
</style>