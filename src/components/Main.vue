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

const addCreatedPostInList = (createdPost) => {
  posts.value.push(createdPost);
};

const updatePostInList = (editedPost) => {
  // O findIndex retorna a posição caso a regra retorne true, ou caso não encontre nenhum item com a regra aplicada, retorna -1
  const indexOfPostInList = posts.value.findIndex(
    (item) => item.id === editedPost.id// regra
  );
  console.log('Posição', indexOfPostInList)

  if (indexOfPostInList !== -1) {
    // já que encontrou o post existente no array de posts, edita ele
    posts.value[indexOfPostInList] = editedPost;
  }
};


const quantidadeDePosts = ref(10)
</script>

<template>
  <AddButton @showCreationEmit="creationForm = !creationForm" />
  <!--<Case @showUpdate="updateForm = !updateForm" v-for="post in posts" :name="post.title" :body="post.body" class="case"  :key="post.id" />-->
  <Case @showUpdate="[(updateForm = !updateForm), (postData = post), dale()]" v-for="(post, postIndex) in posts"
    :name="post.title" :body="post.body" class="case" :key="post.id" v-show="postIndex + 1 <= quantidadeDePosts" />
  <button @click="quantidadeDePosts += 10">Ver mais</button>

  <Creation v-if="creationForm" @success="addCreatedPostInList" @close="creationForm = false" />
  <!--<Update v-if="updateForm" v-for="post in posts" :nameValue="post.title" :textValue="post.body"/> -->
  <Update v-if="updateForm" :post="postData" @success="updatePostInList" @close="updateForm = false" />
</template>

<style scoped>
.case {
  margin: 5px;
  display: flex;
  display: inline-block;
  cursor: pointer;
}
</style>
