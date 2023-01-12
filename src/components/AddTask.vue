<script setup>
import { ref } from 'vue'
const emit = defineEmits(['taskAdded', 'closeModal'])

const title = ref('')
const deadline = ref('')


function addTask() {
    emit('taskAdded', title.value)
}

</script>

<template>
    <div class="inset-0 fixed backdrop-blur bg-black bg-opacity-20">
        <div class="flex  flex-col w-full h-full justify-end">
            <div class="relative bg-white rounded-t-3xl p-4">
                <button  @click="$emit('closeModal')" class="absolute top-4 right-4 opacity-30">
                    <svg fill="#000000" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="24px" height="24px">
                        <path
                            d="M 4.7070312 3.2929688 L 3.2929688 4.7070312 L 10.585938 12 L 3.2929688 19.292969 L 4.7070312 20.707031 L 12 13.414062 L 19.292969 20.707031 L 20.707031 19.292969 L 13.414062 12 L 20.707031 4.7070312 L 19.292969 3.2929688 L 12 10.585938 L 4.7070312 3.2929688 z" />
                    </svg>
                </button>
                <h1 class="font-bold text-2xl text-center py-3">Add task</h1>
                <input v-model="title" type="text" placeholder="Name" class="w-full my-2 border-slate-200 border rounded-lg p-2">
                <div class="flex justify-between text-slate-400 text-sm">
                    <button
                        class="border-slate-200 border rounded-lg p-2 py-2 px-3.5 active:bg-indigo-600 active:text-white">
                        Today
                    </button>
                    <button
                        class="border-slate-200 border rounded-lg p-2 py-2 px-3.5 active:bg-indigo-600 active:text-white">
                        Tomorrow
                    </button>
                    <button
                        class="border-slate-200 border rounded-lg p-2 py-2 px-3.5 active:bg-indigo-600 active:text-white">
                        This weekend
                    </button>
                    <button class="border-slate-200 border rounded-lg p-2 active:bg-indigo-600 group">
                        <img src="../assets/images/planner.png" alt=""
                            class="h-6 w-6 opacity-30 group-active:invert group-active:opacity-100">
                    </button>
                </div>
                <div class="flex justify-end py-7 text-slate-400">
                    <label for="priority" class="px-2">High priority</label>
                    <input type="checkbox" id="priority" name="" value="" class="opacity-60 w-5">
                </div>
                <div class="">
                    <button 
                        @click="addTask"
                        class="w-full rounded-lg py-4 bg-indigo-600 text-white font-bold">
                        Add task
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>