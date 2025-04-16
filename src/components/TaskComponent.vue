<script setup>
defineProps({
    title: {
        type: String,
        required: true
    },
    isDone: {
        type: Boolean,
        required: false
    }
})
const emit = defineEmits(['toggle'])
</script>

<template>
    <div id="task-container">
        <p id="title-txt">{{title}}</p>
        <input type="checkbox" :checked="isDone" @change="emit('toggle')">
    </div>
</template>

<style scoped>
#task-container {
    height: 50px;
    width: 90%;
    border: 1px solid gray;
    margin-left: 5%;
    margin-top: 15px;
    border-radius: 10px;
    display: flex;
    justify-content: space-between;
}
#task-container p {
    font-size: 25px;
    margin-top: 10px;
}
#task-container input {
    height: 20px;
    width: 20px;
    margin-top: 15px;
    margin-right: 15px;
    cursor: pointer;
}
#task-container input {
    margin-right: 25px;
}
#title-txt {
    margin-left: 25px;
}
</style>