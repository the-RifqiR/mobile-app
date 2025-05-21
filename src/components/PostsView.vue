<script setup>
import axios from 'axios';
import { onMounted, reactive } from 'vue';
import { useRoute, RouterLink } from 'vue-router';

const route = useRoute();
const postId = route.params.id;
const state = reactive({
    post: Object
})

onMounted(async () => {
    try {
        const response = await axios.get(`http://localhost/belajar-api/get-all-data.php?id=${postId}`);
        state.post = response.data;
    } catch (error) {
        console.log("Error while fetching: ", error);
    }
})
</script>

<template>
    <div class="view-container">
        <h1 class="glitch-title">Detail Postingan</h1>
        <div class="content-box">
            <div class="info-group">
                <label>Nama:</label>
                <p class="glitch-text" :data-text="state.post.student_name">{{ state.post.student_name }}</p>
            </div>
            <div class="info-group">
                <label>Nomor:</label>
                <p class="glitch-text" :data-text="state.post.student_no">{{ state.post.student_no }}</p>
            </div>
            <div class="info-group">
                <label>Kelas:</label>
                <p class="glitch-text" :data-text="state.post.student_class">{{ state.post.student_class }}</p>
            </div>
        </div>
        <RouterLink :to="`/posts`" class="btn btn-back">
            <span class="glitch-text" data-text="Kembali">Kembali</span>
        </RouterLink>
    </div>
</template>

<style scoped>
.view-container {
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

.content-box {
    background-color: rgba(255, 255, 255, 0.05);
    border-radius: 10px;
    padding: 20px;
    margin-bottom: 20px;
}

.info-group {
    margin-bottom: 20px;
}

.info-group:last-child {
    margin-bottom: 0;
}

label {
    display: block;
    color: rgba(255, 255, 255, 0.7);
    margin-bottom: 8px;
    font-size: 1.1em;
}

.glitch-text {
    color: white;
    font-size: 1.2em;
    margin: 0;
    padding: 10px;
    background-color: rgba(255, 255, 255, 0.1);
    border-radius: 8px;
    border: 2px solid rgba(255, 255, 255, 0.3);
    position: relative;
}

.glitch-text::before,
.glitch-text::after {
    content: attr(data-text);
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(255, 255, 255, 0.1);
    border-radius: 8px;
    padding: 10px;
    box-sizing: border-box;
}

.glitch-text::before {
    left: 2px;
    text-shadow: -2px 0 #ff00ff;
    animation: glitch-anim-1 2s infinite linear alternate-reverse;
}

.glitch-text::after {
    left: -2px;
    text-shadow: 2px 0 #00ffff;
    animation: glitch-anim-2 3s infinite linear alternate-reverse;
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
    display: inline-block;
}

.btn:hover {
    background-color: rgba(255, 255, 255, 0.1);
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    border-color: rgba(255, 255, 255, 0.5);
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

@keyframes glitch-anim-1 {
    0% {
        clip-path: inset(20% 0 30% 0);
    }
    20% {
        clip-path: inset(60% 0 10% 0);
    }
    40% {
        clip-path: inset(40% 0 50% 0);
    }
    60% {
        clip-path: inset(80% 0 5% 0);
    }
    80% {
        clip-path: inset(10% 0 70% 0);
    }
    100% {
        clip-path: inset(30% 0 20% 0);
    }
}

@keyframes glitch-anim-2 {
    0% {
        clip-path: inset(15% 0 35% 0);
    }
    20% {
        clip-path: inset(55% 0 15% 0);
    }
    40% {
        clip-path: inset(45% 0 45% 0);
    }
    60% {
        clip-path: inset(75% 0 10% 0);
    }
    80% {
        clip-path: inset(15% 0 65% 0);
    }
    100% {
        clip-path: inset(25% 0 25% 0);
    }
}

/* Responsive Styles */
@media screen and (max-width: 768px) {
    .view-container {
        padding: 20px;
        margin: 10px;
    }

    .content-box {
        padding: 15px;
    }

    .glitch-text {
        font-size: 1.1em;
        padding: 8px;
    }

    .btn {
        width: 100%;
        text-align: center;
    }
}

@media screen and (max-width: 480px) {
    .view-container {
        padding: 15px;
        margin: 5px;
    }

    .glitch-title {
        font-size: 1.5em;
        margin-bottom: 20px;
    }

    .info-group {
        margin-bottom: 15px;
    }

    label {
        font-size: 1em;
    }

    .glitch-text {
        font-size: 1em;
        padding: 6px;
    }
}
</style>