<template>
  <div>
    <ul>
      <li v-for="post of posts" :key="post.id">
        <n-link :to="`/posts/${post.id}`">
          {{ post.title }}
        </n-link>
      </li>
      <li>
        <n-link to="/posts/404">
          404 post
        </n-link>
      </li>
    </ul>
    <button @click="printPosts">Print Posts</button>
  </div>
</template>

<script>
export default {
  async fetch () {
    const posts = await this.$axios
      .get('https://jsonplaceholder.typicode.com/posts')
      .then(posts => posts.data.slice(0, 20))
    this.$store.commit('SET_POSTS', posts)
  },
  data () {
    return {
      ok: null
    }
  },
  computed: {
    posts () {
      return this.$store.state.posts
    }
  },
  methods: {
    printPosts () {
      console.log(this.posts)
    }
  }
}
</script>
