<script>
export default {
    name: "Card",
    props: {
        title: {
            type: String,
            required: true,
        },
        done: {
            type: Boolean,
            required: true,
        },
        id: {
            type: Number,
            required: true,
        }
    },
    emits: ["DoneTask"],
}
</script>

<template>
<div class="todo-item__container">
    <div class="todo-item__task">
        {{ title }}
    </div>
    <label>
        <div :id="id" @click="$emit('DoneTask', $event.target.id)" class="todo-item__button" :class="{'todo-item__button--done': done}">
            Done
        </div>
    </label>
</div>
</template>

<style lang="scss">
.todo-item__container {
    display: flex;
    justify-content: space-between;
    box-shadow: 0 0 30px 2px gray;
    padding: 30px;
    color: rgba(255, 255, 255, 0.87);
    border-radius: 15px;
    width: 50vw;
    min-height: 50px;
    transition-duration: 0.5s;
    gap: 1%;
    label div {
        color: green;
        background-color: #1a1a1a;
    }
    &:hover {
        box-shadow: 0 0 30px 2px white;
    }
    .todo-item__button--done {
        color: #1a1a1a;
        background-color: green;
        transform: translateY(4px);
        box-shadow: 0 0 30px 0.5px green;
    }
    .todo-item__button {
        width: 5vw;
        height: 50px;
        border: 1px solid transparent;
        border-radius: 8px;
        font-weight: 500;
        font-family: inherit;
        font-size: 1.2vw;
        display: flex;
        justify-content: center;
        align-items: center;
        &:hover {
            outline: none;
            box-shadow: 0 0 15px 0.3px green;
        }
        &:active {
            color: #1a1a1a;
            background-color: green;
            transform: translateY(4px);
            box-shadow: 0 0 30px 0.5px green;
        }
    }
}
</style>
