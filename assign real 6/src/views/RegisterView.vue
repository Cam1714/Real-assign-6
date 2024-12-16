<script setup>
import { useRegistrationStore } from '../stores';
import { useRouter } from 'vue-router';
import Header from '../components/Header.vue'
import Footer from '../components/Footer.vue'

const store = useRegistrationStore();
const router = useRouter();

const validateForm = (event) => {
  if (store.password !== store.rePassword) {
    event.preventDefault();
    alert('The passwords do not match. Please check and try again.');
  } else {
    store.setRegistrationData({
      firstName: store.firstName,
      lastName: store.lastName,
      email: store.email,
      password: store.password,
    });

    router.push('/movies')
  }
};
</script>

<template>
  <Header />
  <div class="form-container">
    <h2>Create an Account</h2>
    <form @submit="validateForm">
      <input type="text" placeholder="First Name" class="input-field" v-model="store.firstName" required />
      <input type="text" placeholder="Last Name" class="input-field" v-model="store.lastName" required />
      <input type="email" placeholder="Email" class="input-field" v-model="store.email" required />
      <input type="password" placeholder="Password" class="input-field" v-model="store.password" required />
      <input type="password" placeholder="Re-Enter Password" class="input-field" v-model="store.rePassword" required />
      <button type="submit" class="register">Register</button>
    </form>
  </div>
  <Footer />
</template>

<style scoped>
body {
  body {
    background-color: #f3e5f5;
    /* Soft pastel purple background */
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    margin: 0;
    font-family: 'Poppins', sans-serif;
  }

  .form-container {
    background-color: #ffffff;
    /* White background for form */
    padding: 40px 30px;
    border-radius: 15px;
    box-shadow: 0 12px 24px rgba(0, 0, 0, 0.1);
    width: 100%;
    max-width: 400px;
    text-align: center;
  }

  h2 {
    font-size: 2rem;
    color: #333;
    margin-bottom: 20px;
  }

  .input-field {
    padding: 15px;
    font-size: 1rem;
    width: 100%;
    border: 1px solid #ccc;
    border-radius: 10px;
    background-color: #f9f9f9;
    transition: all 0.3s ease;
  }

  .input-field:focus {
    border-color: #4CAF50;
    box-shadow: 0 0 8px rgba(76, 175, 80, 0.4);
    outline: none;
  }

  .register {
    background-color: #4CAF50;
    color: white;
    padding: 12px 20px;
    border: none;
    border-radius: 10px;
    font-size: 1.1rem;
    cursor: pointer;
    transition: background-color 0.3s, transform 0.2s;
  }

  .register:hover {
    background-color: #45a049;
    transform: scale(1.05);
  }

  .register:active {
    background-color: #388e3c;
  }
}
</style>