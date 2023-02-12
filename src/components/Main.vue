<template>
    <AddButton @showCreationEmit="creationForm = !creationForm" />
    <Case :name="post.title" :body="post.body" class="case" v-for="post in posts" :key="post.id" />
    <Creation v-if="creationForm" />

</template>

<script setup>
import { onMounted, ref } from 'vue'

import AddButton from "./AddButton.vue"
import Case from "./Case.vue"
import Creation from "./Creation.vue"

const props = defineProps({
    name: String,
    body: String
})

onMounted(() => {
    Getposts()
})

const Getposts = async () => {
    const data = await fetch('http://localhost:3000/posts')
    const res = await data.json()
    posts.value = res
}

const posts = ref([])

let creationForm = ref(false)




</script>

<style scoped>
.case {
    margin: 5px;
    display: flex;
    display: inline-block;
    cursor: pointer;


}
</style>

