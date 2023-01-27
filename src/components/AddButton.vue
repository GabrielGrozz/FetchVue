<template>
    <div>
        <div>
            <button @click="sendEmit">Criar</button>
        </div>
    </div>
</template>

<script setup>
const emit = defineEmits(['showCreationEmit'])

const sendEmit = () => {
    emit('showCreationEmit')
}

</script>

<style scoped>

</style>