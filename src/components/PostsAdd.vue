<script setup>
import axios from 'axios';
import { reactive } from 'vue';
import { RouterLink, useRouter } from 'vue-router';

const router = useRouter();

const form = reactive({
    student_name: '',
    student_class: '',
    student_no: ''
})

const handleSubmit = async () => {
    const newPost = {
        student_name: form.student_name,
        student_class: form.student_class,
        student_no: form.student_no
    }
    try {
        const response = await axios.post('http://localhost/belajar-api/insert-data.php', newPost);
        console.log('Response:', response.data);
        router.push('/posts');
    } catch (error) {
        console.error("Error on posting data:", error);
    }
}
</script>

<template>
    <div class="form-container">
        <h1 class="glitch-title">Tambah Postingan</h1>
        <RouterLink :to="`/posts`" class="btn btn-back">
            <span class="glitch-text" data-text="Kembali">Kembali</span>
        </RouterLink>
        <form @submit.prevent="handleSubmit" class="glitch-form">
            <div class="form-group">
                <label for="name">Nama</label>
                <input v-model="form.student_name" type="text" id="name" name="name" placeholder="Masukan Nama" class="glitch-input">
            </div>
            <div class="form-group">
                <label for="class">Kelas</label>
                <input v-model="form.student_class" type="text" id="class" name="class" placeholder="Masukan Kelas" class="glitch-input">
            </div>
            <div class="form-group">
                <label for="no">Nomor</label>
                <input v-model="form.student_no" type="text" id="no" name="no" placeholder="Masukan Nomor" class="glitch-input">
            </div>
            <button type="submit" class="btn btn-submit">
                <span class="glitch-text" data-text="Submit">Submit</span>
            </button>
        </form>
    </div>
</template>

<style scoped>
.form-container {
    max-width: 800px;
    margin: 0 auto;
    padding: 30px;
    background-color: rgba(255, 255, 255, 0.05);
    backdrop-filter: blur(10px);
    border-radius: 15px;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
}

.glitch-title {
    color: white;
    margin-bottom: 30px;
    text-align: center;
    font-size: 2em;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    animation: titleGlitch 5s infinite;
}

.form-group {
    margin-bottom: 20px;
}

label {
    display: block;
    color: white;
    margin-bottom: 8px;
    font-size: 1.1em;
}

.glitch-input {
    width: 100%;
    padding: 12px;
    background-color: rgba(255, 255, 255, 0.1);
    border: 2px solid rgba(255, 255, 255, 0.3);
    border-radius: 8px;
    color: white;
    font-size: 1em;
    transition: all 0.3s ease;
}

.glitch-input:focus {
    outline: none;
    border-color: rgba(255, 255, 255, 0.5);
    background-color: rgba(255, 255, 255, 0.15);
    box-shadow: 0 0 15px rgba(255, 255, 255, 0.1);
}

textarea.glitch-input {
    min-height: 150px;
    resize: vertical;
}

.btn {
    padding: 12px 24px;
    border-radius: 8px;
    text-decoration: none;
    font-weight: 500;
    transition: all 0.3s ease;
    background-color: transparent;
    color: white;
    border: 2px solid rgba(255, 255, 255, 0.3);
    cursor: pointer;
    font-size: 1em;
}

.btn:hover {
    background-color: rgba(255, 255, 255, 0.1);
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    border-color: rgba(255, 255, 255, 0.5);
}

.btn-submit {
    margin-top: 20px;
    width: 100%;
}

@keyframes titleGlitch {
    0%, 100% {
        text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    }
    25% {
        text-shadow: -2px 2px 4px #ff00ff;
    }
    50% {
        text-shadow: 2px -2px 4px #00ffff;
    }
    75% {
        text-shadow: -2px -2px 4px #ff00ff;
    }
}

/* Responsive Styles */
@media screen and (max-width: 768px) {
    .form-container {
        padding: 20px;
        margin: 10px;
    }

    .form-group {
        margin-bottom: 15px;
    }

    .glitch-input {
        padding: 10px;
        font-size: 0.9em;
    }

    textarea.glitch-input {
        min-height: 120px;
    }

    .btn {
        width: 100%;
        text-align: center;
    }

    .btn-back {
        margin-bottom: 15px;
    }
}

@media screen and (max-width: 480px) {
    .form-container {
        padding: 15px;
        margin: 5px;
    }

    .glitch-title {
        font-size: 1.5em;
        margin-bottom: 20px;
    }

    label {
        font-size: 1em;
    }

    .glitch-input {
        padding: 8px;
        font-size: 0.9em;
    }

    textarea.glitch-input {
        min-height: 100px;
    }
}
</style>