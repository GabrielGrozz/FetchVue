<template>
    <div class="case-container">
        <div class="name">
            <h1>{{ name }}</h1>
        </div>
        <div class="body">
            <p>{{ body }}</p>
        </div>
        <button class="button">Editar</button>
    </div>
</template>

<script setup>
//forma como passamos props com composition API
const props = defineProps({
    name: String,
    body: String
})

const emit = defineEmits([
    "gabriel", "alex"])

console.log(props.name)
</script>

<style scoped>
.case-container {
    position: relative;
    margin: 3px;
    background-color: black;
    height: 200px;
    width: 150px;
    ;
    border: 2px red solid;
    padding: 5px;
}

.name {
    color: rgb(117, 55, 55);
    font-size: 10px;
    white-space: nowrap;
    overflow: hidden;
}

.body {
    color: rgb(155, 150, 236);
    overflow: hidden;
    border: 2px red solid;
    height: 60%;
}

.button {
    position: absolute;
    bottom: 5px;
    right: 5px;
}
</style>