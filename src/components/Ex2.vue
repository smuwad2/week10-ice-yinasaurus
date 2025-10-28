<script>
import axios from 'axios'
import BlogPost from './subcomponents/BlogPost.vue'

export default {
  components: { BlogPost },
  data() {
    return {
      posts: [] // array of post objects
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
  }
}
</script>

<template>
    <blog-post v-for="post in posts" :subject="post.subject" 
    :entry="post.entry" :mood="post.mood" :key="post.id"></blog-post>
</template>
