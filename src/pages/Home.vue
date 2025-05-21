<!-- eslint-disable vue/multi-word-component-names -->
// eslint-disable-next-line vue/multi-word-component-names
<script setup>
import { RouterLink } from 'vue-router';
</script>

<template>
    <div class="home-container">
        <div class="content-wrapper">
            <h1 class="glitch-title">Selamat Datang di Web CRUD Vue.</h1>
            <RouterLink :to="`/login`" class="btn btn-enter">
                <span class="glitch-text" data-text="Masuk">Masuk</span>
            </RouterLink>
        </div>
    </div>
</template>

<style scoped>
.home-container {
    min-height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}

.content-wrapper {
    text-align: center;
    padding: 2rem;
    background-color: rgba(255, 255, 255, 0.05);
    border-radius: 15px;
    backdrop-filter: blur(10px);
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.3);
}

.glitch-title {
    color: white;
    font-size: 2.5rem;
    margin-bottom: 2rem;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.3);
    animation: titleGlitch 5s infinite;
}

.btn-enter {
    display: inline-block;
    padding: 12px 30px;
    background-color: transparent;
    color: white;
    text-decoration: none;
    border-radius: 8px;
    font-size: 1.1rem;
    font-weight: 500;
    transition: all 0.3s ease;
    border: 2px solid rgba(255, 255, 255, 0.3);
}

.btn-enter:hover {
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

/* Responsive Styles */
@media screen and (max-width: 768px) {
    .home-container {
        padding: 20px;
    }

    .content-wrapper {
        padding: 20px;
    }

    .glitch-title {
        font-size: 2em;
    }

    .btn {
        width: 100%;
        text-align: center;
    }
}

@media screen and (max-width: 480px) {
    .home-container {
        padding: 15px;
    }

    .content-wrapper {
        padding: 15px;
    }

    .glitch-title {
        font-size: 1.5em;
    }

    .btn {
        padding: 10px 20px;
        font-size: 0.9em;
    }
}
</style>