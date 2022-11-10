<template>
  <div v-for="gif in gifs">
    {{ gif.title }}
    <!-- Cross origin issue on the image, will fix this later -->
    <!-- <img :src="gif.embed_url" /> -->
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

<style scoped></style>
