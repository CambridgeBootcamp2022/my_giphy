<template>
  <div v-for="gif in gifs">
    <span>{{ gif.title }}</span>
    <a :href="gif.embed_url" target="_blank">View GIF</a>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'MyGiphy',
  data() {
    return {
      gifs: [],
    }
  },
  created() {
    this.getTrendingGifs()
  },
  methods: {
    async getTrendingGifs() {
      const giphy = await axios.get(
        'https://api.giphy.com/v1/gifs/trending?api_key=SvCwcwJxMMsZnJ2WEQU0rwXBXJJdKaN1'
      )
      this.gifs = giphy.data.data

      // async-await doesn't work on fetch!
      //   fetch(
      //     'https://api.giphy.com/v1/gifs/trending?api_key=SvCwcwJxMMsZnJ2WEQU0rwXBXJJdKaN1'
      //   )
      //     .then((response) => response.json())
      //     .then((data) => (this.gifs = data.data))
    },
  },
}
</script>

<style scoped>
a {
  color: #4caf50;
}

div {
  padding: 2rem;
  margin: 2rem;
  display: flex;
  flex-direction: column;
  justify-content: center;
  border: 1px solid #ccc;
  border-radius: 4px;
}
</style>
