<template>
  <div>
    <SearchJokes @search-text="searchText" />
    <Joke v-for="j in jokes" :id="j.id" :key="j.id" :joke="j.joke" />
  </div>
</template>

<script>
import axios from 'axios'
import Joke from '../../components/Joke'
import SearchJokes from '../../components/SearchJokes'

export default {
  components: {
    Joke,
    SearchJokes
  },
  data() {
    return {
      jokes: []
    }
  },
  async created() {
    const config = {
      headers: {
        'Accept': 'application/json'
      }
    }

    try {
      const res = await axios.get('https://icanhazdadjoke.com/search', config)
      /* eslint-disable no-console */
      console.log(res.data)
      /* eslint-enable no-console */

      this.jokes = res.data.results
    } catch (err) {
      /* eslint-disable no-console */
      console.log(err)
      /* eslint-enable no-console */
    }
  },
  methods: {
    async searchText(text) {
      const config = {
        headers: {
          'Accept': 'application/json'
        }
      }

      try {
        const res = await axios.get(`https://icanhazdadjoke.com/search?term=${text}`, config)
        /* eslint-disable no-console */
        console.log(res.data)
        /* eslint-enable no-console */

        this.jokes = res.data.results
      } catch (err) {
        /* eslint-disable no-console */
        console.log(err)
        /* eslint-enable no-console */
      }
    }
  },
  head() {
    return {
      title: 'Dad jokes',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Best place for corny dad jokes'
        }
      ]
    }
  }
}
</script>

<style>

</style>
