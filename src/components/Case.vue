<template>
  <div class="case-container">
    <div class="name">
      <h1>{{ name }}</h1>
    </div>
    <div class="body">
      <p class="body-content">{{ body }}</p>
    </div>
    <button class="button" @click="showUpdate">Editar</button>
  </div>
</template>

<script setup>
import { ref } from "vue";

//forma como passamos props com composition API
const props = defineProps({
  name: String,
  body: String,
});

const nameValue = ref(props.name);

const emit = defineEmits(["showUpdate"]);
const showUpdate = () => {
  emit("showUpdate");
};
</script>

<style scoped>
.case-container {
  position: relative;
  margin: 3px;
  background-color: black;
  height: 200px;
  width: 150px;
  border: 2px red solid;
  padding: 5px;
}

.name {
  color: rgb(117, 55, 55);
  font-size: 10px;
  white-space: nowrap;
  overflow: hidden;
}

.body {
  color: rgb(155, 150, 236);
  overflow: hidden;
  height: 60%;
  background: rgba(149, 149, 149,.2);


}

.body-content{
  display: -webkit-box;
    -webkit-line-clamp: 6;
    -webkit-box-orient: vertical;

}

.button {
  position: absolute;
  bottom: 5px;
  right: 5px;
}
</style>
