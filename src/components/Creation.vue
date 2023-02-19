<template>
  <div class="modal">
    <div class="modal-content">
      <form action="" @submit.prevent="createBurger" class="form">
        <label class="label" for="name">Nome</label>
        <input type="text" name="name" id="name" v-model="name" />

        <label class="label" for="content">Conteudo</label>
        <textarea name="content" id="content" v-model="content"></textarea>

        <button class="saveContent" type="submit">Salvar</button>
        <button @click="emit('close')" type="button"> X </button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const emit = defineEmits(["success", "close"]);

let name = ref(null);
let content = ref(null);

const verificaSeEValido = () => {
  if (!name.value || !content.value) {
    return false
  }
  if (name.value.length < 3) {
    return false
  }
  return true
}

const createBurger = async () => {
  if(verificaSeEValido() === false) {
    alert('Preencha os dados corretamente')
    return
  }
  const data = {
    title: name.value,
    body: content.value,
  };
  const dataJSON = JSON.stringify(data);

  const req = await fetch("http://localhost:3000/posts", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: dataJSON,
  });

  const res = await req.json();
  console.log(res);

  emit("success", res);
  emit('close')
};
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  align-items: center;
}

label {
  margin: 5px 0;
}

#name {
  margin-bottom: 20px;
}

#content {
  position: relative;
  resize: none;
  width: 90%;
  height: 150px;
}
</style>
