<template>
  <div>
    <header>
      <nav>
        <ul>
          <li @click="currentTab = 'Post'" :class="{ active: currentTab === 'Post' }">Post</li>
          <li @click="currentTab = 'TodoList'" :class="{ active: currentTab === 'TodoList' }">TodoList</li>
        </ul>
      </nav>
    </header>

    <div v-if="currentTab === 'Post'">
      <Post />
    </div>

    <div v-else-if="currentTab === 'TodoList'">
      <TodoList />
    </div>

    <div v-else>
      <p>Content for other tabs...</p>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
import Post from './components/Post.vue';
import TodoList from './components/ToDos.vue';

export default {
  components: { Post, TodoList },
  setup() {
    const currentTab = ref('Post'); // Set tab awal ke "Post"
    return { currentTab };
  }
};
</script>

<style>
.active {
  font-weight: bold;
}
</style>
