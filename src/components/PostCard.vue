<script setup>
import { TrashIcon } from "@heroicons/vue/24/outline";
defineProps(["post"]);
const emit = defineEmits(["delete"]);
</script>

<template>
  <article class="card">
    <header>
      <img :src="post.author.avatarUrl" alt="Avatar" width="36" height="36" class="avatar" />
      <a>{{ post.author.username }}</a>
    </header>
    <p>{{ post.content }}</p>

    <footer>
      <button class="btn-icon trash-icon" @click="emit('delete', post.id)">
        <TrashIcon />
      </button>
    </footer>
  </article>
</template>
