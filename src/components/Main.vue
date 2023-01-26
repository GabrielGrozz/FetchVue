<template>
    <AddButton />
    <Case :name="post.title" :body="post.body" class="case" v-for="post in posts" :key="post.id" />

</template>

<script setup>
import { onMounted, ref } from 'vue'

import AddButton from "./AddButton.vue"
import Case from "./Case.vue"

const props = defineProps({
    name: String,
    body: String
})

onMounted(() => {
    Getposts()
})

const posts = ref([])

const Getposts = async () => {
    const data = await fetch('http://localhost:3000/posts')
    const res = await data.json()
    console.log(res)
    posts.value = res
}



</script>

<style scoped>
.case {
    margin: 5px;
    display: flex;
    display: inline-block;

    cursor: pointer;


}
</style>

