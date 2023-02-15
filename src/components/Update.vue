<template>
  <div class="update-container">
    <form action="" @submit.prevent="updatePost">
      <label for="name">Nome</label><br />
      <input type="text" name="name" id="name" v-model="nameValue" /><br />

      <label for="text">Anotação</label><br />
      <textarea
        name="text-area"
        id="text"
        cols="30"
        rows="10"
        v-model="textValue"
      ></textarea
      ><br />

      <button @click="() => {}">Deletar</button>
      <button type="submit">Salvar alterações</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from "vue";

const nameValue = ref('sdaasaddd')
const textValue = ref("latcaracao twitter")
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
