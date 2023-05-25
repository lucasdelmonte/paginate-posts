<script setup>
  import { ref, onMounted } from 'vue'
  import BlogPost from './components/BlogPost.vue'
  import paginatePost from './components/PaginatePost.vue'
  import loadingSpinner from './components/LoadingSpinner.vue'
  import reguestError from './components/RequestError.vue'

  const posts = ref([])
  const postForPage = 10
  const init = ref(0)
  const end = ref(postForPage)
  const loading = ref(true)
  const requestPostsError = ref(false)

  const favorite = ref('')

  const next = () => {
    init.value += postForPage
    end.value += postForPage
  }
  const prev = () => {
    init.value -=  postForPage
    end.value -= postForPage
  }

  // Example using onMounted()
  /*
  onMounted(async () => {
    try {
      const res = await fetch('https://jsonplaceholder.typicode.com/posts')
      posts.value = await res.json()
    } catch (e) {
      requestPostsError.value = true
    } finally {
      setTimeout(() => loading.value = false, 2000)
    }
  })
  */

  // Recommended method to consume APIs
  const fetchData = async () => {
    try {
      const res = await fetch('https://jsonplaceholder.typicode.com/posts')
      posts.value = await res.json()
    } catch (e) {
      requestPostsError.value = true
    } finally {
      setTimeout(() => loading.value = false, 2000)
    }
  }
  fetchData()

  const changeFavorite = (title) => favorite.value = title
</script>

<template>
  <loadingSpinner v-if="loading" />
  <div class="container" v-else-if="!loading && !requestPostsError">
    <h1>My posts</h1>
    <h2>Favorite post: {{ favorite }}</h2>

    <paginatePost
      @next="next"
      @prev="prev"
      :init="init"
      :end="end"
      :maxLength="posts.length"
    />

    <BlogPost
      v-for="(post, index) in posts.slice(init , end)"
      :key="index"
      :title="post.title"
      :id="post.id"
      :body="post.body"
      @changeFavorite="changeFavorite"
    >
    </BlogPost>
  </div>
  <reguestError v-else />
</template>