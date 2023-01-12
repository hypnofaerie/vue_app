<script setup>
import { ref, computed } from 'vue'
const months = [
    'January',
    'February',
    'March',
    'April',
    'May',
    'June',
    'July',
    'August',
    'September',
    'October',
    'November',
    'December'
]

const selected = ref('January')
const selectedDay = ref(1)

const daysOfWeek = [
    'Sun',
    'Mon',
    'Tue',
    'Wed',
    'Thu',
    'Fri',
    'Sat'
]

function getDaysInMonth(year, month) {
    return new Date(year, month, 0).getDate()
}

const daysInCurrentMonth = computed(() => {
    const days = []
    let monthIndex = months.findIndex((element) => element === selected.value)
    let numberOfDays = getDaysInMonth(2022, monthIndex + 1)

    const firstDayDate = new Date(selected.value + ' 1, 2022 23:15:30')
    let firstDay = firstDayDate.getDay()

    for (let index = 1; index <= numberOfDays; index++) {
        days.push(
            {
                dayNumber: index,
                dayName: daysOfWeek[firstDay]
            }
        )
        firstDay += 1
        if (firstDay > 6) firstDay = 0
    }
    return days
})

const currentDate = computed(() => {
    return {
        day: selectedDay.value,
        month: selected.value.slice(0, 3)
    }
})

function changeDay(day) {
    selectedDay.value = day
} 
</script>

<template>
    <section class="text-white px-3">
        <div class="flex justify-between mt-2">
            <h2 class="font-bold text-2xl py-2">To-do list</h2>
            <button class="bg-white text-indigo-600 rounded-lg px-2 basis-12">
                <p class="font-bold">
                    {{ currentDate.day }}
                </p>
                <p>
                    {{ currentDate.month }}
                </p>
            </button>
        </div>
        <div>
            <select v-model="selected" class="bg-transparent mt-2 -ml-1">
                <option v-for="month in months" class="text-indigo-600">{{ month }}</option>
            </select>
            <div class="py-3 flex flex-nowrap gap-x-4 overflow-auto">
                <button v-for="day in daysInCurrentMonth" 
                    @click="changeDay(day.dayNumber)"
                    class=" bg-white bg-opacity-20 focus:bg-opacity-100 focus:text-indigo-600 rounded-lg py-2 basis-12 shrink-0">
                    <p class="font-bold leading-tight text-lg">{{ day.dayNumber }}</p>
                    <p class="text-xs">{{ day.dayName }}</p>
                </button>
            </div>
        </div>
    </section>
</template>