<script setup>
import { computed, ref } from "vue";
import PostCard from "@/components/PostCard.vue";

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
    liked: false, // Initial state for like
  };
  posts.value.push(newPost);
  text.value = "";
}

function deletePost(id) {
  const postElement = document.getElementById(id);
  if (postElement) {
    postElement.classList.add("removing");
    setTimeout(() => {
      posts.value = posts.value.filter((post) => post.id !== id);
    }, 500);
  }
}

function likePost(id) {
  const post = posts.value.find((post) => post.id === id);
  if (post) {
    post.liked = !post.liked;
  }
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

      <PostCard
        v-for="post in [...posts].reverse()"
        :key="post.id"
        :post="post"
        @delete="deletePost"
        @like="likePost"
      />
    </div>
  </main>
</template>
