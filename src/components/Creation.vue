<template>
  <div class="creation-container">
    <div class="creation">
      <form action="" @submit="createBurger" class="form">
        <label class="label" for="name">Nome</label>
        <input type="text" name="name" id="name" v-model="name" />

        <label class="label" for="content">Conteudo</label>
        <textarea name="content" id="content" v-model="content"></textarea>

        <button class="saveContent" type="submit">Salvar</button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

let name = ref(null);
let content = ref(null);

const createBurger = async () => {
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

  console.log(data);
};
</script>

<style scoped>
.creation-container {
  display: flex;
  justify-content: center;
  align-items: center;
}

.creation {
  position: absolute;
  height: 300px;
  width: 400px;
  top: 20%;
  background: purple;
  padding: 10px;
}

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
