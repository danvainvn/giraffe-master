<template>
    <div>
        <h2>Danh sách bài viết</h2>
        <ul>
            <li v-for="post in posts" :key="post.id">
                {{ post.title }} - {{ post.author }}
            </li>
        </ul>
    </div>
</template>

<script>
import axios from 'axios';
export default {
    data() {
        return {
            posts: []
        };
    },
    mounted() {
        this.fetchPosts();
    },
    methods: {
        async fetchPosts() {
            try {
                const response = await axios.get('http://localhost:3000/posts');
                this.posts = response.data;
                this.posts.forEach(post => {
                    console.log(`Title: ${post.title}, Author: ${post.author}`);
                });
            } catch (error) {
                console.error('Lỗi khi lấy dữ liệu:', error);
            }
        }
    }
};
</script>
