
<script>
import axios from 'axios'
import BlogPost from './subcomponents/BlogPost2.vue'

export default {
  components: { BlogPost },
  data() {
    return {
      posts: []
    }
  },
  computed: {
    baseUrl() {
      if (window.location.hostname === 'localhost')
        return 'http://localhost:3000'
      else {
        const codespace_host = window.location.hostname.replace('5173', '3000')
        return `https://${codespace_host}`
      }
    }
  },
  created() {
    axios.get(`${this.baseUrl}/posts`)
      .then(response => {
        this.posts = response.data
      })
      .catch(error => {
        this.posts = [{ subject: 'Error', entry: 'There was an error: ' + error.message, mood: 'error' }]
      })
  },
  methods: {
    deletePost(id) {
      axios.get(`${this.baseUrl}/deletePost`, { params: { id } })
        .then(() => {
          this.posts = this.posts.filter(post => post.id !== id)
        })
        .catch(error => {
          alert('Delete failed: ' + error.message)
        })
    }
  }
}
</script>

<template>
  <div class="container mt-4">
    <h3>Blog Posts</h3>

    <!-- Vertical stack: one card per line -->
    <div v-for="post in posts" :key="post.id" class="mb-3">
      <BlogPost 
        :id="post.id"
        :subject="post.subject"
        :entry="post.entry"
        :mood="post.mood"
      >
        <!-- Slot content: Delete button -->
        <button 
          class="btn btn-danger mt-2"
          @click="deletePost(post.id)"
        >
          Delete
        </button>
      </BlogPost>
    </div>
  </div>
</template>
