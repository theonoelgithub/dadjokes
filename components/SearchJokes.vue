
<template>
  <form @submit.prevent="onSubmit">
    <input v-model="text" type="text" placeholder="Search Jokes...">
    <input type="submit" value="Search Jokes">
  </form>
</template>

<script>
export default {
  name: 'SearchJokes',
  data() {
    return {
      text: ''
    }
  },
  methods: {
    onSubmit() {
      // emit the event to the parent
      this.$emit('search-text', this.text)
      this.text = ''
    }
  }
}
</script>

<style>
</style>
