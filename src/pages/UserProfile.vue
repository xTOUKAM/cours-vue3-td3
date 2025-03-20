<script setup>
import { useRoute } from "vue-router";

const { params } = useRoute();
const username = params.username;
const title = "User profile";
</script>

<template>
  <h1>{{ title }}</h1>
  <h2>{{ username }}</h2>
</template>
