<script setup>
import { computed, ref } from "vue";

const text = ref("");
const trimmedText = computed(() => text.value.trim());
const posts = ref([]);

function addPost() {
  const newPost = {
    id: Math.random().toString(36).substring(2),
    content: trimmedText.value,
    createdAt: new Date(),
    author: {
      id: Math.random().toString(36).substring(2),
      username: "TOUKAM",
      avatarUrl: "https://i.pravatar.cc/2002",
    },
  };
  posts.value.push(newPost);
  text.value = "";
}
</script>

<template>
  <main>
    <div class="container">
      <form action="" class="card" @submit.prevent="addPost">
        <textarea name="post" id="post" placeholder="Quoi de neuf?" v-model="text"></textarea>
        <button type="submit" :disabled="!trimmedText">Publier</button>
      </form>

      <p v-if="!posts.length">Pas de post pour le moment.</p>

      <article v-for="post in [...posts].reverse()" :key="post.id" class="card">
        <div class="post-header">
          <img
            :src="post.author.avatarUrl"
            alt="Avatar"
            width="40"
            height="40"
            class="user-image"
          />
          <a>{{ post.author.username }}</a>
        </div>
        <p>{{ post.content }}</p>
      </article>
    </div>
  </main>
</template>

<style scoped>
.container {
  height: 100vh;
  margin: 0 auto;
  max-width: 640px;
}
.card {
  background-color: var(--color-bg-secondary);
  border-radius: 10px;
  border: 1px solid var(--color-border);
  margin-bottom: 1rem;
}

form {
  display: flex;
  flex-direction: column;
  margin-top: 1rem;
  padding: 1rem 1.5rem;
  width: 100%;
}
textarea {
  background: none;
  border: none;
  color: var(--color-text-primary);
  flex: 1;
  margin-bottom: 1rem;
  outline: none;
  padding: 0.5rem 0;
  resize: none;
  field-sizing: content;
}
button {
  align-self: flex-end;
  background: none;
  border-radius: 10px;
  border: 1px solid var(--color-border);
  color: var(--color-text-primary);
  cursor: pointer;
  font-size: 1rem;
  height: 40px;
  padding: 0 1rem;
}

button:disabled {
  cursor: not-allowed;
  opacity: 0.4;
}

button:hover {
  transition: background-color 0.3s;
  background-color: var(--color-bg-tertiary);
}

article {
  padding: 0.75rem 1.5rem;
  overflow: hidden;
}

article p {
  white-space: pre-wrap;
}

.user-image {
  border-radius: 50%;
  object-fit: cover;
}

.post-header {
  align-items: center;
  display: flex;
  margin-bottom: 1rem;
  gap: 1rem;
}
</style>
