<template>
  <div class="update-container">
    <form action="" @submit.prevent="updatePost">
      <label for="name">Nome</label><br />
      <input
        type="text"
        name="name"
        id="name"
        v-model="propsValue.title"
      /><br />

      <label for="text"></label><br />
      <textarea
        name="text-area"
        id="text"
        cols="30"
        rows="10"
        v-model="propsValue.body"
      ></textarea
      ><br />

      <button>Deletar</button>
      <button type="submit" @click="updatePost">Salvar alterações</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from "vue";

const props = defineProps({
  post: Object,
});

const propsValue = ref(props.post);

const updatePost = async () => {
  const req = await fetch(`http://localhost:3000/posts/${propsValue.value.id}`, {
    method: "PUT",
    body: JSON.stringify(propsValue),
    headers: { "Content-Type": "application/json" },
  });
  const res = req.json()
  console.log(res)
};
</script>

<style scoped>
.update-container {
  width: 400px;
  height: 400px;
  background: red;
  position: absolute;
  top: 150px;
  left: 400px;
}
</style>
