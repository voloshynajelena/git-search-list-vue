<template>
  <tr>
    <td>{{ data.name }}</td>
    <td>{{ data.description }}</td>
    <td><a :href=' data.homepage '>{{ data.homepage }}</a></td>
    <td>
      <button @click='removeField(index)'>&times;</button>
    </td>
  </tr>
</template>

<script>

export default {
  name: 'list',
  props: ['data', 'index'],
  methods: {
    removeField (index) {
      this.$emit('remove-item', index)
    }
  }
}
</script>

<style>
</style>
