<template>
    <div>
        <input type='text' ref='title' v-model='query' autofocus placeholder='Git search' />
        <button @click='gitSearch(query)'>&#128269;</button>
    </div>
</template>

<script>

export default {
  name: 'FieldSearch',
  data () {
    return {
      query: ''
    }
  },
  methods: {
    gitSearch (query) {
      this.$emit('git-search', query)
    }
  }
}
</script>

<style>
</style>
