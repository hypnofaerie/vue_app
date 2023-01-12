<script setup>
import {ref} from 'vue'
import Nav from './components/Nav.vue'
import Calendar from './components/Calendar.vue'
import Tasks from './components/Tasks.vue' 
</script>

<template>
    <Nav />
    <main>
        <Calendar />
        <Tasks />
    </main>
</template>

<style scoped>

</style>