<script setup>
import { useRouter } from 'vue-router';
import { ref } from 'vue';
import { useRegistrationStore } from '../stores';
import Header from '../components/Header.vue'
import Footer from '../components/Footer.vue'

const store = useRegistrationStore();
const email = ref('');
const password = ref('');
const router = useRouter();

const handleLogin = () => {
  if (email.value === store.email && password.value === store.password) {
    router.push("/movies");
  } else {
    alert('Login incorrect :(');
  }
};
</script>

<template>
  <Header />
  <div class="hero">
    <div class="overlay">
      <div class="form-container">
        <h2>Login to Your Account</h2>
        <form @submit.prevent="handleLogin">
          <input v-model="email" type="email" placeholder="Email" class="input-field" required />
          <input v-model="password" type="password" placeholder="Password" class="input-field" required />
          <button type="submit" class="button login">Login</button>
        </form>
      </div>
    </div>
  </div>
  <Footer />
</template>

<style scoped>
.hero {
  background-image: url('background.webp');
  background-size: cover;
  background-position: center;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.overlay {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  background: rgba(0, 0, 0, 0.5);
  padding: 20px;
  border-radius: 12px;
}

.form-container {
  background-color: #ffffff;
  padding: 40px;
  border-radius: 12px;
  box-shadow: 0 4px 15px rgba(0, 0, 0, 0.1);
  width: 100%;
  max-width: 420px;
}

h2 {
  font-size: 2rem;
  color: #333;
  text-align: center;
  margin-bottom: 24px;
}

.input-field {
  width: 100%;
  padding: 14px;
  margin: 12px 0;
  border: 1px solid #ddd;
  border-radius: 8px;
  font-size: 1rem;
  background-color: #f7f7f7;
  color: #333;
}

.input-field:focus {
  border-color: #5e81ac;
  outline: none;
}

.button {
  width: 100%;
  padding: 16px;
  background-color: #5e81ac;
  color: white;
  border: none;
  border-radius: 8px;
  font-size: 1.2rem;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.button:hover {
  background-color: #4c6b8c;
}

.logo {
  font-size: 2rem;
  font-family: 'Georgia', serif;
  font-style: italic;
  font-weight: bold;
  margin-left: 8px;
  color: #ff7043;
}
</style>
