<script setup>
import { ref, reactive } from 'vue'
import AddTask from './AddTask.vue' 

const showAddTask = ref(false)

let tasks = reactive([])
let completed = reactive([])
let currentTab = ref('active')

function moveToCompleted(index) {
    const deletedItems = tasks.splice(index, 1)
    completed.push(deletedItems[0])
}

function moveToActive(index) {
    const deletedItems = completed.splice(index, 1)
    tasks.push(deletedItems[0])
}

function taskAdded(title) {
    console.log(title);
    tasks.push({title: title})
    showAddTask.value = false
}
</script>

<template>
    <section class="bg-slate-50 rounded-t-lg mt-3 p-3 pt-5" style="height: calc(100vh - 299px);">
        <div class="flex flex-cols-2 place-content-around  gap-x-2">
            <button @click="currentTab = 'active'"
                :class="currentTab == 'active' ? 'border-indigo-600 font-semibold' : 'border-transparent'"
                class="hover:border-indigo-600 hover:font-semibold  border-b-2 w-full pb-2">
                Active tasks
                <span class="hover:text-indigo-600 focus:text-indigo-600 text-black bg-slate-200 rounded px-2 text-sm">
                    {{ tasks.length }}
                </span>
            </button>
            <button @click="currentTab = 'completed'"
                :class="currentTab == 'completed' ? 'border-indigo-600 font-semibold' : 'border-transparent'"
                class="hover:border-indigo-600 hover:font-semibold  border-b-2 w-full pb-2">
                Completed
                <span class="hover:text-indigo-600 focus:text-indigo-600 text-black bg-slate-200 rounded px-2 text-sm">
                    {{ completed.length }}
                </span>
            </button>
        </div>
        <div v-if="currentTab == 'active'" class="overflow-auto" 
            style="height: calc(100% - 22px);">
            <p v-show="tasks.length == 0" class="p-3 text-center">
                No active tasks
            </p>
            <ul class="py-4 leading-tight">
                <li v-for="(task, i) in tasks" @click="moveToCompleted(i)"
                    class="relative flex justify-between items-center p-4 mb-4 font-bold bg-white rounded-lg shadow-md">
                    <div>
                        <p>
                            {{ task.title }}
                        </p>
                        <span class="text-xs font-normal text-indigo-600">
                            {{ task.deadline }}
                        </span>
                    </div>
                    <div class="w-8">
                        <svg width="30px" height="30px" viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg">
                            <path fill="#4f46e5"
                                d="M256 23.05C127.5 23.05 23.05 127.5 23.05 256S127.5 488.9 256 488.9 488.9 384.5 488.9 256 384.5 23.05 256 23.05zm0 17.9c118.9 0 215.1 96.15 215.1 215.05S374.9 471.1 256 471.1c-118.9 0-215.05-96.2-215.05-215.1C40.95 137.1 137.1 40.95 256 40.95z" />
                        </svg>
                    </div>
                </li>
            </ul>
        </div>
        <div v-if="currentTab == 'completed'" class="overflow-auto" 
            style="height: calc(100% - 22px);">
            <p v-show="completed.length == 0" class="p-3 text-center">
                No completed tasks
            </p>
            <ul class="py-4 leading-tight">
                <li v-for="(task, i) in completed" @click="moveToActive(i)"
                    class="relative flex justify-between items-center p-4 mb-4 font-bold bg-white rounded-lg shadow-md">
                    <div>
                        <p>
                            {{ task.title }}
                        </p>
                        <span class="text-xs font-normal text-indigo-600">
                            {{ task.deadline }}
                        </span>
                    </div>
                    <div class="relative w-8">
                        <svg width="30px" height="30px" viewBox="0 0 512 512" xmlns="http://www.w3.org/2000/svg">
                            <path fill="#4f46e5"
                                d="M256 23.05C127.5 23.05 23.05 127.5 23.05 256S127.5 488.9 256 488.9 488.9 384.5 488.9 256 384.5 23.05 256 23.05zm0 17.9c118.9 0 215.1 96.15 215.1 215.05S374.9 471.1 256 471.1c-118.9 0-215.05-96.2-215.05-215.1C40.95 137.1 137.1 40.95 256 40.95z" />
                        </svg>
                        <svg class="p-2 absolute h-full w-full inset-0" version="1.1" xmlns="http://www.w3.org/2000/svg" x="0px" y="0px" width="78.369px" height="78.369px"
                            viewBox="0 0 78.369 78.369" style="enable-background:new 0 0 78.369 78.369;" xml:space="preserve">
                            <g>
                                <path d="M78.049,19.015L29.458,67.606c-0.428,0.428-1.121,0.428-1.548,0L0.32,40.015c-0.427-0.426-0.427-1.119,0-1.547l6.704-6.704
                        		c0.428-0.427,1.121-0.427,1.548,0l20.113,20.112l41.113-41.113c0.429-0.427,1.12-0.427,1.548,0l6.703,6.704
                        		C78.477,17.894,78.477,18.586,78.049,19.015z" />
                            </g>
                        </svg>
                    </div>
                </li>
            </ul>
        </div>
        <AddTask v-show="showAddTask" 
            @close-modal="showAddTask = false" 
            @task-added="taskAdded"
            />
        <div v-show="!showAddTask" class="fixed bottom-4 right-4">
            <button @click="showAddTask = !showAddTask" class="rounded-lg p-2 bg-indigo-600 text-white font-bold">
                <img src="../assets/images/plus.png" alt="" class="invert h-8">
            </button>
        </div>
    </section>

</template>  

<style scoped>
</style>