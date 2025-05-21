<!-- eslint-disable vue/multi-word-component-names -->
// eslint-disable-next-line vue/multi-word-component-names
<script setup>
import axios from 'axios';
import { RouterLink, useRouter } from 'vue-router';

const router = useRouter();
    
const props = defineProps({
    post: Object
});

const deletePost = async (postId) => {
    try {
        const confirm = window.confirm('Are you sure you want to delete this posts?');
        if(confirm) {
            await axios.delete(`http://localhost/belajar-api/delete-data.php?student_id=${postId}`);
            console.log(confirm);
            router.push('/');
        }
    } catch (error) {
        console.error("Error deleting post: ", error);
    }
}
</script>

<template>
    <tr>
        <td>{{ post.student_id }}</td>
        <td>{{ post.student_no }}</td>
        <td>{{ post.student_name }}</td>
        <td>{{ post.student_class }}</td>
        <td class="action-cell">
            <RouterLink :to="`/posts/${post.student_id}`" class="btn btn-view" title="View Details">
                <span class="icon">👁️</span>
            </RouterLink>
            <RouterLink :to="`/posts/edit/${post.student_id}`" class="btn btn-edit" title="Edit Data">
                <span class="icon">✏️</span>
            </RouterLink>
            <button @click="deletePost(post.student_id)" class="btn btn-delete" title="Delete Data">
                <span class="icon">🗑️</span>
            </button>
        </td>
    </tr>
</template>

<style scoped>
.action-cell {
    display: flex;
    gap: 8px;
}

.btn {
    padding: 8px 12px;
    border-radius: 4px;
    border: 2px solid rgba(255, 255, 255, 0.3);
    background-color: transparent;
    color: white;
    cursor: pointer;
    font-weight: 500;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
}

.icon {
    font-size: 1.2em;
}

.btn-view {
    color: #4CAF50;
}

.btn-edit {
    color: #2196F3;
}

.btn-delete {
    color: #f44336;
}

.btn:hover {
    background-color: rgba(255, 255, 255, 0.1);
    transform: translateY(-2px);
    box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
    border-color: rgba(255, 255, 255, 0.5);
}

.btn-view:hover {
    background-color: rgba(76, 175, 80, 0.1);
}

.btn-edit:hover {
    background-color: rgba(33, 150, 243, 0.1);
}

.btn-delete:hover {
    background-color: rgba(244, 67, 54, 0.1);
}
</style>