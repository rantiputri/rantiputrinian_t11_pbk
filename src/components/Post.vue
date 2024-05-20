<template>
  <div>
    <h2>Post</h2>

    <!-- User selection -->
    <h3>Select User:</h3>
    <select v-model="selectedUser" @change="loadPosts">
      <option value="" disabled>Select User</option>
      <option v-for="user in users" :key="user.id" :value="user.id">{{ user.name }}</option>
    </select>

    <!-- Post listing -->
    <div v-if="selectedUser">
      <h3>Posts by {{ users.find(user => user.id === selectedUser).name }}:</h3>
      <ul>
        <li v-for="post in posts" :key="post.id">
          <h4>{{ post.title }}</h4>
          <p>{{ post.body }}</p>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from 'vue';

export default {
  setup() {
    const users = ref([]);
    const selectedUser = ref(null);
    const posts = ref([]);

    const loadUsers = async () => {
      const response = await fetch('https://jsonplaceholder.typicode.com/users');
      const data = await response.json();
      users.value = data;
    };

    const loadPosts = async () => {
      if (selectedUser.value) {
        const response = await fetch(`https://jsonplaceholder.typicode.com/posts?userId=${selectedUser.value}`);
        const data = await response.json();
        posts.value = data;
      }
    };

    onMounted(loadUsers);

    return { users, selectedUser, posts, loadPosts };
  }
};
</script>
