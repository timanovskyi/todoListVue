<template>
  <form @submit="submit">
    <input type="text" name="name" v-model="title">
    <button type="submit">create</button>
  </form>
</template>

<script>

export default {
  data() {
    return {
      title: ''
    }
  },
  methods: {
    submit(event) {
      event.stopPropagation();
      event.preventDefault();
      this.$emit('create-item', this.title.trim())
      this.title = '';
    }
  }
}
</script>
