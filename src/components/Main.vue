<script setup>
import { onMounted, ref } from "vue";

import AddButton from "./AddButton.vue";
import Case from "./Case.vue";
import Creation from "./Creation.vue";
import Update from "./Update.vue";

const updateForm = ref(false);
const creationForm = ref(false);
const postData = ref(null);

const props = defineProps({
  name: String,
  body: String,
});

const dale = () => {
  console.log(postData.value);
};

onMounted(() => {
  Getposts();
});

const posts = ref([]);

const Getposts = async () => {
  const data = await fetch("http://localhost:3000/posts");
  const res = await data.json();
  posts.value = res;
};
</script>

<template>
  <AddButton @showCreationEmit="creationForm = !creationForm" />
  <!--<Case @showUpdate="updateForm = !updateForm" v-for="post in posts" :name="post.title" :body="post.body" class="case"  :key="post.id" />-->
  <Case
    @showUpdate="[(updateForm = !updateForm), (postData = post), dale()]"
    v-for="post in posts"
    :name="post.title"
    :body="post.body"
    class="case"
    :key="post.id"
  />
  <Creation v-if="creationForm" />
  <!--<Update v-if="updateForm" v-for="post in posts" :nameValue="post.title" :textValue="post.body"/> -->
  <Update
    v-if="updateForm"
    :post="postData"
  />
</template>

<style scoped>
.case {
  margin: 5px;
  display: flex;
  display: inline-block;
  cursor: pointer;
}
</style>
