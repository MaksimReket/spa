<script>
import { Card } from "../components";
import axios from 'axios';

export default {
    name: "ToDoList",
    components: { Card },
    data() {
        return {
            data: [],
        };
    },
    async mounted() {
        // localStorage.clear()
        const storedData = localStorage.getItem('todoData')
        if (storedData) {
            this.data = JSON.parse(storedData)
        } else {
            const response = await axios.get("data.json")
            console.log(response.data)
            this.data = response.data
            localStorage.setItem('todoData', JSON.stringify(this.data))
        }
    },
    methods: {
        doneTask(id) {
            const index = this.data.findIndex(i => i.id === Number(id))
            this.data[index].done = !this.data[index].done
            localStorage.setItem('todoData', JSON.stringify(this.data))
            console.log(this.data)
        },
    },
}
</script>

<template>
    <div class="todo-list__container">
        <Card
            v-for="task in data"
            :key="task.id"
            @done-task="doneTask"
            :title="task.title"
            :done="task.done"
            :id="task.id"
        />
    </div>
</template>

<style>
.todo-list__container {
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 1%;
    gap: 2vh;
}
</style>