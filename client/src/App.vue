<script setup>
import TodoList from "./components/TodoList.vue";
import axios from "axios";
import { ref } from "vue";

const title = ref("");

async function sendPost() {
  const response = await axios.post(`http://localhost:3000/todos`, {
    // id: Date.now(),
    title: title.value,
    completed: false,
  });
  console.log(response);
}
</script>

<template>
  <v-container>
    <h1>To Dos App</h1>
    <v-container class="card">
      <v-form ref="form">
        <input type="text" placeholder="saisir votre todo" v-model="title" />
        <v-btn variant="flat" color="green" @click="sendPost">Ajouter</v-btn>
      </v-form>
    </v-container>
    <v-container>
      <TodoList></TodoList>
    </v-container>
  </v-container>
</template>

<style scoped></style>
