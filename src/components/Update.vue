<template>
  <div class="update-container">
    <form action="" @submit="updatePost">
      <label for="name">Nome</label><br />
      <input
        type="text"
        name="name"
        id="name"
        v-model="propsValue.title"
      /><br />

      <label for="text"></label><br />
      <textarea
        name="text"
        id="text"
        cols="30"
        rows="10"
        v-model="propsValue.body"
      ></textarea
      ><br />

      <button @click="DeletePost">Deletar</button>
      <button type="submit" @click="updatePost">Salvar alterações</button>
    </form>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const emit = defineEmits(["success"]);

const props = defineProps({
  post: Object,
});

const propsValue = ref(JSON.parse(JSON.stringify(props.post)));

const updatePost = async () => {
  const req = await fetch(
    `http://localhost:3000/posts/${propsValue.value.id}`,
    {
      method: "PUT",
      body: JSON.stringify(propsValue.value),
      headers: { "Content-Type": "application/json" },
    }
  );
  const res = await req.json();
  emit("success", res);
  console.log(res);
};

const DeletePost = async () => {
  const req = await fetch(`http://localhost:3000/posts/${propsValue.value.id}`, { method: "DELETE"})

  const res = await req.json()
  console.log(res, "delete sucess")
}
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
