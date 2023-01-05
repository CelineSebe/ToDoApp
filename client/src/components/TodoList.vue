<script setup>
import axios from "axios";
import { reactive } from "vue";
import { onMounted } from "vue";

const toDos = reactive({
  posts: [],
});

async function fetchPost() {
  const { data } = await axios.get("http://localhost:3000/todos");
  toDos.posts = data;
  console.log("get", data);
}

async function deletePost(id) {
  await axios.delete(`http://localhost:3000/todos/${id}`);
}

async function modifyPost(id) {
  await axios.patch(`http://localhost:3000/todos/${id}`, {
    completed: true,
  });
}

onMounted(() => {
  fetchPost();
});
</script>

<template>
  <v-container class="d-flex column justify-center">
    <v-form>
      <v-card
        class="d-flex justify-space-between"
        v-for="post of toDos.posts"
        :key="post.id"
      >
        <input type="radio" @click="modifyPost(post.id)" />
        <div>
          <strike v-if="post.completed">{{ post.title }}</strike>
          <span v-else>{{ post.title }}</span>
        </div>
        <v-btn variant="flat" color="error" @click="deletePost(post.id)"
          >Delete</v-btn
        >
      </v-card>
    </v-form>
  </v-container>
</template>
