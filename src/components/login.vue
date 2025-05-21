<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { ref, reactive } from 'vue'
import { useRouter } from 'vue-router'
import axios from 'axios'

const router = useRouter();

// Form reaktif untuk username dan password
const form = reactive({
    username: '',
    password: ''
});

// Menyimpan pesan error jika login gagal
const errorMessage = ref('');

// Fungsi untuk menangani proses login
const handleLogin = async () => {
    try {
        const response = await axios.post('http://localhost/belajar-api/login.php', {
            username: form.username,
            password: form.password
        });

        const result = response.data;

        if (result.status === 'succes') {
            // Login berhasil, arahkan ke halaman posts
            router.push('/posts');
        } else {
            // Login gagal, tampilkan pesan error
            errorMessage.value = result.msg || 'Login gagal!';
        }
    } catch (error) {
        console.error('Login error:', error);
        errorMessage.value = 'Terjadi kesalahan saat login.';
    }
}
</script>

<template>
    <div class="login-page">
      <h2>Login Admin</h2>
      <form @submit.prevent="handleLogin">
        <input v-model="form.username" type="text" placeholder="Username" required />
        <input v-model="form.password" type="password" placeholder="Password" required />
        <button type="submit">Login</button>
        <p v-if="errorMessage" class="error">{{ errorMessage }}</p>
      </form>
    </div>
</template>

<style scoped>
/* Style untuk halaman login */
.login-page {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 100vh;
  background: #f4f7fa;
  font-family: Arial, sans-serif;
}

h2 {
  color: #333;
  font-size: 2rem;
  margin-bottom: 1.5rem;
  text-align: center;
}

/* Form */
form {
  display: flex;
  flex-direction: column;
  width: 100%;
  max-width: 400px;
  padding: 2rem;
  background-color: #fff;
  border-radius: 8px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

/* Input fields */
input {
  padding: 0.75rem;
  margin-bottom: 1rem;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 1rem;
  color: #ffffff;
  transition: border-color 0.3s ease;
}

input:focus {
  border-color: #007bff;
  outline: none;
}

button {
  padding: 0.75rem;
  background-color: #007bff;
  color: #fff;
  font-size: 1rem;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

button:hover {
  background-color: #0056b3;
}

/* Pesan error */
.error {
  color: #ff0000;
  font-size: 0.9rem;
  text-align: center;
  margin-top: 1rem;
}
</style>
