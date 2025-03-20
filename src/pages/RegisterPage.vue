<script setup>
import { ref, computed } from "vue";
import { useRouter } from "vue-router";

const router = useRouter();

const formData = ref({
  username: "",
  email: "",
  password: "",
});

const isSubmitDisabled = computed(() => {
  return !formData.value.username || !formData.value.email || !formData.value.password;
});

const handleSubmit = async () => {
  fetch("https://posts-crud-api.vercel.app/register", {
    method: "POST",
    headers: {
      "Content-Type": "application/json",
    },
    body: JSON.stringify({
      username: formData.value.username,
      email: formData.value.email,
      password: formData.value.password,
    }),
  })
    .then((response) => response.json())
    .then((data) => {
      localStorage.setItem("user", JSON.stringify(data));
      router.push("/");
    });
};
</script>

<template>
  <div>
    <h1>Register</h1>
    <form @submit.prevent="handleSubmit">
      <div>
        <label for="username">Nom d'utilisateur</label>
        <input
          v-model="formData.username"
          type="text"
          id="username"
          placeholder="Entrez votre nom d'utilisateur"
          required
        />
      </div>
      <div>
        <label for="email">Adresse email</label>
        <input
          v-model="formData.email"
          type="email"
          id="email"
          placeholder="Entrez votre email"
          required
        />
      </div>
      <div>
        <label for="password">Mot de passe</label>
        <input
          v-model="formData.password"
          type="password"
          id="password"
          placeholder="Entrez votre mot de passe"
          required
        />
      </div>
      <button type="submit" :disabled="isSubmitDisabled">S'inscrire</button>
    </form>
  </div>
</template>

<style scoped>
h1 {
  text-align: center;
  margin-top: 32px;
  margin-bottom: 16px;
  font-size: 1.5rem;
  color: white;
  text-transform: uppercase;
  letter-spacing: 1px;
}

form {
  max-width: 400px;
  margin: auto;
  padding: 16px;
  border: 1px solid #ccc;
  border-radius: 10px;
}

div {
  margin-bottom: 16px;
}

label {
  display: block;
  font-weight: bold;
}

input {
  width: 100%;
  padding: 8px;
  margin-top: 4px;
  border: 1px solid #ccc;
  border-radius: 4px;

  &:focus {
    outline: none;
    border-color: #3182ce;
  }

  &::placeholder {
    color: #ccc;
    transition: color 0.5s;
  }

  &:invalid {
    border-color: red;
    transition: border-color 0.5s;
  }

  &:hover {
    border-color: #3182ce;
    transition: border-color 0.5s;
  }
}

button {
  width: 100%;
  background-color: #4caf50;
  transition: background-color 0.5s;
}

button:disabled {
  background-color: #ff6961;
  transition: background-color 0.5s;
}
</style>
