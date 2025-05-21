<!-- eslint-disable vue/multi-word-component-names -->
<script setup>
import { onMounted, reactive } from 'vue';
import { RouterLink } from 'vue-router';
import axios from 'axios';
import Post from '@/components/Post.vue';

const state = reactive({
    posts: []
})

onMounted(async () => {
  try {
    const response = await axios.get('http://localhost/belajar-api/get-all-data.php');
    state.posts = response.data;
  } catch (error) {
    console.error('Error fetching jobs:', error);
  }
});

</script>

<template>
     <div class="posts-container">
        <h1 class="glitch-title">Semua Postingan</h1>
        <div class="button-group">
            <RouterLink :to="`/`" class="btn btn-back">
                <span class="glitch-text" data-text="Kembali">Kembali</span>
            </RouterLink>
            <RouterLink :to="`/posts/add`" class="btn btn-add">
                <span class="glitch-text" data-text="Tambahkan Postingan">Tambahkan Postingan</span>
            </RouterLink>
        </div>
        <table id="posts">
            <tr>
                <th>ID</th>
                <th>Nomor</th>
                <th>Nama</th>
                <th>Kelas</th>
                <th>Action</th>
            </tr>
            <Post v-for="post in state.posts" :key="post.id" :post="post"/>
        </table>
     </div>
</template>

<style scoped>
.posts-container {
    max-width: 1000px;
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

.button-group {
    display: flex;
    gap: 10px;
    margin-bottom: 20px;
    justify-content: center;
}

.btn {
    padding: 10px 20px;
    border-radius: 6px;
    text-decoration: none;
    font-weight: 500;
    transition: all 0.3s ease;
    background-color: transparent;
    color: white;
    border: 2px solid rgba(255, 255, 255, 0.3);
}

.btn:hover {
    background-color: rgba(255, 255, 255, 0.1);
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    border-color: rgba(255, 255, 255, 0.5);
}

#posts {
    width: 100%;
    border-collapse: collapse;
    margin-top: 20px;
    background-color: rgba(255, 255, 255, 0.05);
    box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
    border-radius: 8px;
    overflow: hidden;
}

#posts th {
    background-color: rgba(0, 0, 0, 0.3);
    color: white;
    padding: 15px;
    text-align: left;
    font-weight: 600;
}

#posts td {
    padding: 12px 15px;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
    color: white;
}

#posts tr:last-child td {
    border-bottom: none;
}

#posts tr:hover {
    background-color: rgba(255, 255, 255, 0.05);
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
    .posts-container {
        padding: 15px;
    }

    .button-group {
        flex-direction: column;
        gap: 10px;
    }

    .btn {
        width: 100%;
        text-align: center;
    }

    table {
        display: block;
        overflow-x: auto;
        white-space: nowrap;
    }

    th, td {
        padding: 8px;
        font-size: 0.9em;
    }

    .action-cell {
        gap: 4px;
    }

    .btn {
        padding: 6px 10px;
    }
}

@media screen and (max-width: 480px) {
    .posts-container {
        padding: 10px;
    }

    th, td {
        padding: 6px;
        font-size: 0.8em;
    }

    .glitch-title {
        font-size: 1.5em;
    }
}
</style>