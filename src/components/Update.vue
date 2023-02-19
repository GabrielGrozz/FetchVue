<template>
  <div class="modal">
    <form action="" @submit="updatePost" class="modal-content">
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
      <button @click="emit('close')"> X </button>
    </form>e
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const emit = defineEmits(["success", "close"]);

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
  emit("close")
  
};

const DeletePost = async () => {
  const req = await fetch(`http://localhost:3000/posts/${propsValue.value.id}`, { method: "DELETE"})

  const res = await req.json()
  console.log(res, "delete sucess")
  emit("close")
  
}
</script>

<style scoped>
</style>
